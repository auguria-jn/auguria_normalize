# AUGURIA — Génération des tests module Odoo

> **Usage** : Joindre ce fichier + `AUGURIA_MODULE_ODOO.md` + le ZIP du module.
> **Prompt** : `Génère les tests du module joint`
> Ce fichier ne modifie aucun fichier existant du module. Il ajoute uniquement les fichiers de tests.

---

## Instructions pour Claude

Quand l'utilisateur demande de **générer les tests** en joignant ce fichier et un ZIP :

1. **Décompresser** le ZIP et analyser l'intégralité du code source
2. **Identifier** tous les éléments testables (modèles, méthodes, workflows, sécurité, contraintes, vues)
3. **Générer** les fichiers de tests selon les règles ci-dessous
4. **Livrer** le module repackagé en **ZIP** avec le dossier `tests/` complété
5. **Résumer** la couverture de tests générée (nombre de classes, méthodes de test, éléments couverts)

---

## 1. Structure du dossier `tests/`

```
tests/
├── __init__.py
├── common.py                    # Classes de base partagées, données de test
├── test_models.py               # Tests unitaires des modèles (CRUD, compute, contraintes)
├── test_workflows.py            # Tests des workflows et transitions d'état
├── test_security.py             # Tests des droits d'accès et record rules
├── test_business_logic.py       # Tests de la logique métier spécifique
└── test_views.py                # Tests de cohérence des vues XML
```

### Fichier `__init__.py`
```python
# -*- coding: utf-8 -*-
from . import common
from . import test_models
from . import test_workflows
from . import test_security
from . import test_business_logic
from . import test_views
```

### Règles de nommage
- Chaque fichier de test commence par `test_`
- Chaque classe de test hérite de la classe appropriée (voir section 2)
- Chaque méthode de test commence par `test_`
- Nommage explicite : `test_<action>_<contexte>_<résultat_attendu>` (ex: `test_validate_order_sets_state_confirmed`)
- Si un fichier de test n'a aucun contenu pertinent (ex: pas de workflow dans le module), ne pas le créer

---

## 2. Classes de base et données de test — `common.py`

### Structure
```python
# -*- coding: utf-8 -*-
# =============================================================================
# Module : nom_technique_module
# Fichier : tests/common.py
# Description : Classes de base et données de test partagées
# Auteur : AUDURIA by ANOR
# Création : YYYY-MM-DD
# Mise à jour : YYYY-MM-DD
# =============================================================================

from odoo.tests.common import TransactionCase, SavepointCase, tagged


@tagged('post_install', '-at_install')
class NomModuleTestCommon(TransactionCase):
    """
    Classe de base pour les tests du module nom_technique_module.
    Centralise la création des données de test réutilisables.
    """

    @classmethod
    def setUpClass(cls):
        super().setUpClass()

        # =====================================================================
        # Utilisateurs de test
        # =====================================================================
        cls.group_user = cls.env.ref('nom_module.group_nom_module_user')
        cls.group_manager = cls.env.ref('nom_module.group_nom_module_manager')

        cls.user_employee = cls.env['res.users'].with_context(
            no_reset_password=True
        ).create({
            'name': 'Test Utilisateur',
            'login': 'test_user_nom_module',
            'email': 'test_user@example.com',
            'groups_id': [(6, 0, [
                cls.env.ref('base.group_user').id,
                cls.group_user.id,
            ])],
        })

        cls.user_manager = cls.env['res.users'].with_context(
            no_reset_password=True
        ).create({
            'name': 'Test Manager',
            'login': 'test_manager_nom_module',
            'email': 'test_manager@example.com',
            'groups_id': [(6, 0, [
                cls.env.ref('base.group_user').id,
                cls.group_manager.id,
            ])],
        })

        # =====================================================================
        # Données métier de test
        # =====================================================================
        # Créer ici les enregistrements partagés entre les tests
        # cls.record_1 = cls.env['model.name'].create({...})
```

### Principes de `common.py`
- **Centraliser** toutes les données de test (utilisateurs, enregistrements métier)
- **Un utilisateur par groupe** de sécurité défini dans le module
- **Des enregistrements** représentatifs pour chaque modèle principal du module
- **`setUpClass`** : utiliser `@classmethod` pour les données stables (partagées entre tests de la classe)
- **Ne jamais** coder en dur des IDs numériques — toujours utiliser `env.ref()` ou `create()`

---

## 3. Tests unitaires des modèles — `test_models.py`

### Éléments à tester pour chaque modèle

#### 3.1 Création (Create)
```python
def test_create_record_with_required_fields(self):
    """Vérifie la création d'un enregistrement avec les champs obligatoires."""
    record = self.env['model.name'].create({
        'name': 'Test Record',
        # ... champs required
    })
    self.assertTrue(record.exists())
    self.assertEqual(record.name, 'Test Record')
```

#### 3.2 Valeurs par défaut
```python
def test_default_values(self):
    """Vérifie que les valeurs par défaut sont correctement appliquées."""
    record = self.env['model.name'].create({'name': 'Test'})
    self.assertEqual(record.state, 'draft')
    # Tester chaque champ ayant un default=...
```

#### 3.3 Champs compute
```python
def test_compute_field_name(self):
    """Vérifie le calcul du champ <field_name>."""
    record = self.env['model.name'].create({...})
    # Modifier les champs source du @api.depends
    record.write({'source_field': new_value})
    # Vérifier le résultat
    self.assertEqual(record.computed_field, expected_value)
```

#### 3.4 Champs compute inverse
```python
def test_inverse_field_name(self):
    """Vérifie que l'écriture sur le champ compute déclenche l'inverse."""
    record = self.env['model.name'].create({...})
    record.computed_field = new_value
    self.assertEqual(record.source_field, expected_inverse_value)
```

#### 3.5 Contraintes Python (`@api.constrains`)
```python
def test_constrains_field_name_raises(self):
    """Vérifie que la contrainte sur <field> lève une erreur si violée."""
    with self.assertRaises(ValidationError):
        self.env['model.name'].create({
            'field': invalid_value,
        })
```

#### 3.6 Contraintes SQL (`_sql_constraints`)
```python
def test_sql_constraint_unique_name(self):
    """Vérifie la contrainte d'unicité sur <field>."""
    self.env['model.name'].create({'name': 'Unique'})
    with self.assertRaises(IntegrityError):
        # Nécessite un savepoint
        with self.cr.savepoint():
            self.env['model.name'].create({'name': 'Unique'})
```

#### 3.7 Surcharges CRUD
```python
def test_create_generates_sequence(self):
    """Vérifie que create() génère un numéro de séquence."""
    record = self.env['model.name'].create({...})
    self.assertNotEqual(record.name, '/')
    self.assertTrue(record.name.startswith('PREFIX'))

def test_unlink_blocked_in_confirmed_state(self):
    """Vérifie qu'on ne peut pas supprimer un enregistrement confirmé."""
    record = self.env['model.name'].create({...})
    record.action_confirm()
    with self.assertRaises(UserError):
        record.unlink()

def test_write_readonly_field_in_done_state(self):
    """Vérifie que les champs verrouillés ne sont plus modifiables."""
    # Selon la logique métier du module
```

#### 3.8 Onchange
```python
def test_onchange_partner_sets_address(self):
    """Vérifie que le changement de partenaire met à jour l'adresse."""
    record = self.env['model.name'].new({
        'partner_id': self.partner.id,
    })
    record._onchange_partner_id()
    self.assertEqual(record.address, self.partner.street)
```

### Règle de couverture
- **1 test minimum** par champ `compute` avec `@api.depends`
- **1 test minimum** par `@api.constrains`
- **1 test minimum** par `_sql_constraints`
- **1 test** par surcharge `create`, `write`, `unlink` si elles contiennent de la logique
- **1 test** par `@api.onchange`
- **1 test** par valeur `default` non triviale (lambda, fonction)

---

## 4. Tests des workflows — `test_workflows.py`

### Parcours nominal complet
```python
def test_full_workflow_draft_to_done(self):
    """Teste le parcours complet : brouillon → confirmé → terminé."""
    record = self.env['model.name'].create({...})
    self.assertEqual(record.state, 'draft')

    record.action_confirm()
    self.assertEqual(record.state, 'confirmed')

    record.action_done()
    self.assertEqual(record.state, 'done')
```

### Transitions interdites
```python
def test_cannot_skip_confirm_step(self):
    """Vérifie qu'on ne peut pas passer directement de brouillon à terminé."""
    record = self.env['model.name'].create({...})
    with self.assertRaises((UserError, ValidationError)):
        record.action_done()
```

### Annulation et retour
```python
def test_cancel_from_confirmed(self):
    """Vérifie l'annulation depuis l'état confirmé."""
    record = self.env['model.name'].create({...})
    record.action_confirm()
    record.action_cancel()
    self.assertEqual(record.state, 'cancelled')

def test_reset_to_draft_from_cancelled(self):
    """Vérifie le retour en brouillon après annulation."""
    record = self.env['model.name'].create({...})
    record.action_confirm()
    record.action_cancel()
    record.action_reset_to_draft()
    self.assertEqual(record.state, 'draft')
```

### Règle de couverture
- **1 test** pour le parcours nominal complet (happy path)
- **1 test** par transition d'état définie dans le module
- **1 test** par transition interdite (vérifier qu'elle lève une erreur)
- **1 test** pour l'annulation si elle existe
- **1 test** pour le retour en brouillon si il existe

---

## 5. Tests de sécurité — `test_security.py`

### Droits d'accès (`ir.model.access.csv`)
```python
def test_user_can_read(self):
    """Vérifie qu'un utilisateur standard peut lire les enregistrements."""
    records = self.env['model.name'].with_user(self.user_employee).search([])
    self.assertIsNotNone(records)

def test_user_can_create(self):
    """Vérifie qu'un utilisateur standard peut créer un enregistrement."""
    record = self.env['model.name'].with_user(self.user_employee).create({
        'name': 'Test',
    })
    self.assertTrue(record.exists())

def test_user_cannot_delete(self):
    """Vérifie qu'un utilisateur standard ne peut pas supprimer."""
    record = self.env['model.name'].create({'name': 'Test'})
    with self.assertRaises(AccessError):
        record.with_user(self.user_employee).unlink()

def test_manager_can_delete(self):
    """Vérifie qu'un manager peut supprimer."""
    record = self.env['model.name'].create({'name': 'Test'})
    record.with_user(self.user_manager).unlink()
    self.assertFalse(record.exists())
```

### Record rules
```python
def test_user_sees_only_own_company_records(self):
    """Vérifie que la record rule filtre par société."""
    # Créer des enregistrements dans différentes sociétés
    # Vérifier que l'utilisateur ne voit que ceux de sa société
```

### Règle de couverture
- **1 test par combinaison** (groupe × opération CRUD) définie dans `ir.model.access.csv`
- **1 test par record rule** définie dans les fichiers XML de sécurité
- Tester les cas **autorisé** et **refusé**

---

## 6. Tests de la logique métier — `test_business_logic.py`

### Méthodes d'action
```python
def test_action_method_produces_expected_result(self):
    """Teste que <action_method> produit le résultat attendu."""
    record = self.env['model.name'].create({...})
    result = record.action_method()
    # Vérifier l'état après l'action
    # Vérifier les enregistrements créés/modifiés
    # Vérifier la valeur de retour (si action window, etc.)
```

### Wizard
```python
def test_wizard_applies_changes(self):
    """Teste que le wizard applique les modifications sur les enregistrements cibles."""
    records = self.env['model.name'].create([{...}, {...}])
    wizard = self.env['model.wizard'].with_context(
        active_model='model.name',
        active_ids=records.ids,
    ).create({
        'field': value,
    })
    wizard.action_apply()
    # Vérifier les modifications sur records
    for record in records:
        self.assertEqual(record.field, expected_value)
```

### Calculs et montants
```python
def test_amount_computation_with_lines(self):
    """Vérifie le calcul des montants avec plusieurs lignes."""
    record = self.env['model.name'].create({...})
    record.write({'line_ids': [
        (0, 0, {'quantity': 2, 'price_unit': 10.0}),
        (0, 0, {'quantity': 3, 'price_unit': 5.0}),
    ]})
    self.assertAlmostEqual(record.amount_total, 35.0, places=2)

def test_amount_computation_empty_lines(self):
    """Vérifie que le montant est 0 sans lignes."""
    record = self.env['model.name'].create({...})
    self.assertAlmostEqual(record.amount_total, 0.0, places=2)
```

### Cas limites
```python
def test_negative_quantity_raises_error(self):
    """Vérifie qu'une quantité négative lève une erreur."""
    with self.assertRaises((UserError, ValidationError)):
        self.env['model.name'].create({'quantity': -1})

def test_zero_amount_is_allowed(self):
    """Vérifie qu'un montant à zéro est accepté."""
    record = self.env['model.name'].create({'amount': 0.0})
    self.assertTrue(record.exists())

def test_very_long_name_is_truncated_or_accepted(self):
    """Vérifie le comportement avec une valeur très longue."""
    record = self.env['model.name'].create({'name': 'A' * 500})
    self.assertTrue(record.exists())
```

### Règle de couverture
- **1 test** par méthode publique du modèle (hors CRUD et compute déjà couverts)
- **1 test** par wizard avec `action_apply` ou équivalent
- **1 test** par calcul de montant/total
- **2+ tests** par logique complexe (cas nominal + cas limites)

---

## 7. Tests de cohérence des vues — `test_views.py`

### Validation des vues XML
```python
from odoo.tests.common import TransactionCase, tagged


@tagged('post_install', '-at_install')
class TestViews(TransactionCase):
    """Tests de cohérence des vues XML du module."""

    def test_form_view_loads(self):
        """Vérifie que la vue formulaire se charge sans erreur."""
        view = self.env.ref('nom_module.view_model_form')
        self.assertTrue(view.exists())
        # Vérifier que la vue est valide en demandant les champs
        fields = self.env['model.name'].fields_view_get(
            view_id=view.id, view_type='form'
        )
        self.assertIn('arch', fields)

    def test_list_view_loads(self):
        """Vérifie que la vue liste se charge sans erreur."""
        view = self.env.ref('nom_module.view_model_list')
        self.assertTrue(view.exists())
        fields = self.env['model.name'].fields_view_get(
            view_id=view.id, view_type='tree'
        )
        self.assertIn('arch', fields)

    def test_search_view_loads(self):
        """Vérifie que la vue recherche se charge sans erreur."""
        view = self.env.ref('nom_module.view_model_search')
        self.assertTrue(view.exists())
        fields = self.env['model.name'].fields_view_get(
            view_id=view.id, view_type='search'
        )
        self.assertIn('arch', fields)

    def test_all_actions_have_valid_model(self):
        """Vérifie que toutes les actions pointent vers des modèles existants."""
        actions = self.env['ir.actions.act_window'].search([
            ('res_model', 'like', 'nom_module.%'),
        ])
        for action in actions:
            self.assertIn(
                action.res_model,
                self.env,
                f"L'action {action.name} pointe vers un modèle inexistant : {action.res_model}"
            )
```

### Règle de couverture
- **1 test** par vue XML définie dans le module (form, tree, search, kanban, pivot…)
- **1 test global** pour vérifier que toutes les actions window ont un modèle valide

---

## 8. En-tête des fichiers de test

Chaque fichier de test suit l'en-tête AUGURIA standard :

```python
# -*- coding: utf-8 -*-
# =============================================================================
# Module : nom_technique_module
# Fichier : tests/test_xxx.py
# Description : Tests [catégorie] — [description courte]
# Auteur : AUDURIA by ANOR
# Création : YYYY-MM-DD
# Mise à jour : YYYY-MM-DD
# =============================================================================

from odoo.tests.common import TransactionCase, tagged
from odoo.exceptions import UserError, ValidationError, AccessError


@tagged('post_install', '-at_install')
class TestXxx(NomModuleTestCommon):
    """
    Tests [catégorie] du module nom_technique_module.
    Couvre : [liste des éléments testés]
    """
```

### Imports standards
```python
from odoo.tests.common import TransactionCase, SavepointCase, tagged
from odoo.exceptions import UserError, ValidationError, AccessError
from odoo import fields
from datetime import datetime, date, timedelta
from unittest.mock import patch, MagicMock  # si nécessaire
```

---

## 9. Conventions et bonnes pratiques

### Structure d'un test
Chaque méthode de test suit le pattern **Arrange / Act / Assert** :
```python
def test_example(self):
    """Description fonctionnelle de ce que le test vérifie."""
    # --- Arrange : préparer les données ---
    record = self.env['model.name'].create({...})

    # --- Act : exécuter l'action à tester ---
    record.action_confirm()

    # --- Assert : vérifier le résultat ---
    self.assertEqual(record.state, 'confirmed')
```

### Docstrings
- Chaque méthode de test a une **docstring d'une ligne** décrivant le comportement attendu
- Formuler en français, commençant par "Vérifie que…" ou "Teste que…"

### Assertions recommandées
| Assertion | Usage |
|-----------|-------|
| `assertEqual(a, b)` | Valeur exacte |
| `assertNotEqual(a, b)` | Valeur différente |
| `assertTrue(x)` / `assertFalse(x)` | Booléen |
| `assertIn(a, b)` | Appartenance |
| `assertAlmostEqual(a, b, places=2)` | Montants / flottants |
| `assertRaises(Exception)` | Exception attendue |
| `assertRecordValues(records, values)` | Comparaison multi-enregistrements (Odoo) |

### Ce qu'il ne faut PAS faire
- Ne pas tester le framework Odoo lui-même (ORM, champs standards)
- Ne pas tester les modules tiers dont on dépend
- Ne pas utiliser `time.sleep()` dans les tests
- Ne pas dépendre d'un ordre d'exécution entre classes de test
- Ne pas coder en dur des IDs numériques (`self.env.ref()` à la place)
- Ne pas créer des données dans les tests si elles existent dans `common.py`

### Tags
- Utiliser `@tagged('post_install', '-at_install')` par défaut
- Ajouter des tags spécifiques si nécessaire : `@tagged('post_install', '-at_install', 'slow')` pour les tests longs

---

## 10. Analyse du module et génération

### Processus d'analyse

1. **Lire `__manifest__.py`** : identifier les dépendances, la catégorie
2. **Scanner les modèles** (`models/*.py`) :
   - Lister tous les `_name`, `_inherit`, `_description`
   - Identifier les champs `compute` avec leurs `@api.depends`
   - Identifier les `@api.constrains`, `@api.onchange`
   - Identifier les `_sql_constraints`
   - Identifier les surcharges `create`, `write`, `unlink`, `copy`
   - Identifier les méthodes d'action (`action_*`, `button_*`)
   - Identifier les champs `Selection` avec `state` (workflow)
3. **Scanner la sécurité** (`security/`) :
   - Lire `ir.model.access.csv` pour la matrice de droits
   - Lire les `ir.rule` dans les XML pour les record rules
   - Lister les groupes définis
4. **Scanner les vues** (`views/*.xml`) :
   - Lister toutes les vues par type et modèle
   - Lister les actions window
5. **Scanner les wizards** (`wizard/*.py`) :
   - Identifier les `TransientModel` et leurs méthodes d'action
6. **Générer** les fichiers de test en suivant les règles de couverture de chaque section

### Rapport de couverture

À la livraison, fournir un résumé :

```
## Couverture de tests générée

| Catégorie | Fichier | Classes | Méthodes | Éléments couverts |
|-----------|---------|---------|----------|-------------------|
| Données communes | common.py | 1 | - | 2 utilisateurs, N enregistrements |
| Modèles | test_models.py | N | N | N compute, N contraintes, N CRUD |
| Workflows | test_workflows.py | N | N | N transitions d'état |
| Sécurité | test_security.py | N | N | N droits, N record rules |
| Logique métier | test_business_logic.py | N | N | N méthodes, N wizards |
| Vues | test_views.py | 1 | N | N vues, N actions |
| **Total** | **6 fichiers** | **N** | **N** | |
```

---

## 11. Mise à jour du module

### `__manifest__.py`
Aucune modification nécessaire — Odoo découvre automatiquement les tests dans le dossier `tests/` si `__init__.py` est correctement renseigné.

### Exécution des tests
Les tests se lancent via :
```bash
odoo -d test_db --test-enable --stop-after-init -i nom_module
```
Ou pour un fichier spécifique :
```bash
odoo -d test_db --test-enable --test-tags nom_module --stop-after-init
```

---

## 12. Checklist de validation des tests

- [ ] `tests/__init__.py` importe tous les fichiers de test
- [ ] `common.py` crée un utilisateur par groupe de sécurité du module
- [ ] `common.py` crée des données de test pour chaque modèle principal
- [ ] Chaque champ `compute` a au moins 1 test
- [ ] Chaque `@api.constrains` a au moins 1 test (cas valide + cas invalide)
- [ ] Chaque `_sql_constraints` a au moins 1 test
- [ ] Chaque surcharge CRUD avec logique métier a au moins 1 test
- [ ] Chaque transition d'état du workflow a 1 test
- [ ] Chaque transition interdite a 1 test
- [ ] Chaque combinaison groupe × CRUD a 1 test de sécurité
- [ ] Chaque record rule a au moins 1 test
- [ ] Chaque wizard a au moins 1 test
- [ ] Chaque vue XML a 1 test de chargement
- [ ] En-tête AUGURIA sur chaque fichier de test
- [ ] Docstring sur chaque méthode de test
- [ ] Pattern Arrange / Act / Assert respecté
- [ ] Aucun ID numérique codé en dur
- [ ] Tag `@tagged('post_install', '-at_install')` sur chaque classe

---

*Version : 1.0 — Mars 2026*
