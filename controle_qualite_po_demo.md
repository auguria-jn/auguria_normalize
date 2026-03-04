# Contrôle Qualité — password_manager

> **Module** : Gestionnaire de Mots de Passe
> **Version** : 19.0.1.0.0
> **Date d'audit** : 2026-03-04
> **Auditeur** : Claude (AUGURIA by ANOR)
>
> ⚠️ **Ce fichier est un rapport d'observation. Aucune modification n'a été apportée au code.**
> Pour lancer les corrections, cocher les actions souhaitées et renvoyer ce fichier avec le module en demandant : `Applique les corrections cochées`

---

## Synthèse

| Niveau | Nombre |
|--------|--------|
| 🔴 Critique | 0 |
| 🟠 Important | 3 |
| 🟡 Mineur | 4 |
| 🔵 Info | 2 |
| ✅ Conforme | 27 contrôles passés sans anomalie |

---

## A. Qualité du code Python

### ✅ Contrôles conformes

- A01 — Imports : tous les imports (`base64`, `Fernet`, `logging`, `os`, `models`, `fields`, `api`, `ValidationError`) sont utilisés
- A02 — Tous les champs et variables déclarés sont utilisés
- A03 — Aucune duplication de méthode entre fichiers
- A04 — Aucune méthode ne dépasse 50 lignes
- A06 — Aucun appel SQL brut (`env.cr.execute`) sans paramétrage
- A09 — Tous les champs `compute` possèdent un `@api.depends` valide (`encrypted_password` → `_compute_password`, `shared_group_ids` → `_compute_sharing_summary`, `password_entry_ids` → `_compute_password_count`)
- A10 — Aucun `api.onchange` utilisé là où un `compute` serait plus adapté
- A11 — L'héritage de `res.partner` apporte une valeur réelle (One2many + stat button)

### 🟠 Anomalies importantes

**A05 — Utilisation de `sudo()` dans `get_cipher()`**
- **Fichier** : `models/password_entry.py`, lignes ~35 et ~43
- **Détail** : `env['ir.config_parameter'].sudo().get_param(...)` et `.sudo().set_param(...)` sont utilisés pour lire/écrire la clé de chiffrement. Ce `sudo()` est techniquement justifié (l'utilisateur courant n'a pas forcément accès aux paramètres système), mais il contourne les droits normaux.
- **Impact** : Tout code atteignant `get_cipher()` peut écrire dans les paramètres système, quelle que soit l'identité de l'appelant.
- **Action corrective** :
  - [ ] Documenter explicitement pourquoi ce `sudo()` est nécessaire par un commentaire (déjà partiellement fait) et vérifier qu'aucun chemin d'appel non contrôlé ne peut déclencher `get_cipher()` depuis un contexte utilisateur non fiable.

**A07 — `try/except Exception` trop large dans `_compute_password`**
- **Fichier** : `models/password_entry.py`, ligne ~93
- **Détail** : Le `except Exception` capture indistinctement toutes les erreurs, y compris les erreurs de programmation (ex : `AttributeError`, `TypeError`) qui masqueraient des bugs.
- **Impact** : Des erreurs de développement pourraient passer silencieusement en production avec un mot de passe vide affiché.
- **Action corrective** :
  - [ ] Remplacer par `except (InvalidToken, ValueError) as e:` en important `from cryptography.exceptions import InvalidToken` pour cibler uniquement les erreurs de déchiffrement Fernet.

**D03 — Champs `compute` non stockés déclenchant des recalculs fréquents**
- **Fichier** : `models/password_entry.py`
- **Détail** : `password` (`store=False`) et `sharing_summary` (`store=False`) sont recalculés à chaque lecture d'enregistrement. Pour `password`, c'est incontournable (données sensibles). Pour `sharing_summary`, le stockage pourrait éviter les recalculs sur des listes.
- **Impact** : Sur des listes volumineuses (100+ entrées), chaque affichage de la colonne "Visibilité" déclenche N calculs Python.
- **Action corrective** :
  - [ ] Envisager `store=True` sur `sharing_summary` si les performances de la liste deviennent un problème (déclenche une migration).

### 🟡 Anomalies mineures

**A12 — Chaînes non enveloppées dans `_()`**
- **Fichier** : `models/password_entry.py`, multiples occurrences
- **Détail** : Les messages d'erreur dans `ValidationError` (ex: `"Impossible de chiffrer le mot de passe"`) et les valeurs de champs comme `"Privé"` ne sont pas traduits.
- **Impact** : Le module ne peut pas être traduit dans d'autres langues.
- **Action corrective** :
  - [ ] Envelopper toutes les chaînes utilisateur dans `_()` : `raise ValidationError(_("Impossible de chiffrer le mot de passe : %s") % e)` et `rec.sharing_summary = _("Privé")`

---

## B. Qualité des fichiers XML

### ✅ Contrôles conformes

- B01 — Aucun record en double (tous les `id` sont uniques entre fichiers)
- B02 — La vue héritée `view_partner_form_password` cible `base.view_partner_form` via `ref` — XPath stable
- B03 — Tous les groupes référencés dans les vues (`group_password_manager`, `group_password_user`) sont définis dans `security/password_manager_security.xml`
- B04 — L'action `action_password_entry` pointe vers `password.entry` qui est bien défini
- B05 — Tous les champs référencés dans les vues existent dans les modèles Python correspondants
- B06 — Tous les fichiers XML listés dans le manifest existent dans les dossiers correspondants
- B07 — Aucun fichier XML présent dans les dossiers mais absent du manifest

### 🟡 Anomalies mineures

**B — Menu "Mes mots de passe" pointe vers la même action que "Tous les mots de passe"**
- **Fichier** : `views/password_entry_views.xml`
- **Détail** : `menu_password_my_entries` référence `action_password_entry` sans contexte de filtrage par utilisateur courant.
- **Impact** : L'entrée de menu "Mes mots de passe" affiche tous les mots de passe visibles par l'utilisateur, pas uniquement les siens. Le titre est trompeur.
- **Action corrective** :
  - [ ] Créer une action dédiée avec `domain="[('create_uid', '=', uid)]"` ou ajouter un contexte `{'search_default_my_entries': 1}` avec un filtre de recherche correspondant.

---

## C. Sécurité & droits d'accès

### ✅ Contrôles conformes

- C01 — Le modèle `password.entry` possède des règles d'accès dans `ir.model.access.csv` (Utilisateur et Manager)
- C02 — Aucun `TransientModel` dans ce module
- C04 — La hiérarchie des groupes est cohérente : `group_password_manager` implique `group_password_user` via `implied_ids`

### 🟠 Anomalies importantes

**C03 — Record rule Manager avec domain ouvert `[(1,'=',1)]`**
- **Fichier** : `security/password_manager_security.xml`
- **Détail** : La règle `password_entry_manager_rule` utilise `domain_force = [(1,'=',1)]`, ce qui signifie que les managers voient **toutes** les entrées de tous les utilisateurs.
- **Impact** : Comportement intentionnel selon la spécification du module (les managers ont accès complet). Toutefois, il convient de valider que ce niveau d'accès est bien voulu par le client. Un manager mal intentionné peut lire tous les mots de passe de tous les collaborateurs.
- **Action corrective** :
  - [ ] Valider avec le commanditaire que l'accès total du Manager est bien le comportement attendu et documenter cette décision de conception dans le code.

---

## D. Performance

### ✅ Contrôles conformes

- D01 — Aucun `.search()` ou `.browse()` dans une boucle
- D02 — Aucun `.write()` enregistrement par enregistrement (les méthodes `create` et `write` traitent des listes)
- D04 — La méthode `_compute_password` ne fait pas de `.search()` supplémentaire
- D05 — Le modèle `password.entry` possède `_order = "description"`

### 🔵 Informations

**D03 — Champ `password` volontairement non stocké**
- **Détail** : Le champ `password` (compute, store=False) est recalculé à chaque lecture. C'est une décision de sécurité correcte (ne pas stocker le clair). Aucune action requise, mais à garder en tête lors d'optimisations futures.

---

## E. Architecture & bonnes pratiques Odoo

### ✅ Contrôles conformes

- E01 — Aucune logique métier dans un contrôleur
- E02 — Aucun wizard dans ce module
- E03 — Le fichier `data/password_manager_data.xml` est vide avec `noupdate="1"` — pas de données de démo mélangées avec la production
- E04 — `_name = "password.entry"` correspond au nom de table attendu `password_entry`
- E05 — Tous les modèles ont un `_description` (`"Entrée de mot de passe"`)
- E06 — Aucun champ `Selection` avec valeurs en dur
- E07 — `_rec_name = "description"` est explicitement défini sur `PasswordEntry`

### 🟡 Anomalies mineures

**E — Fichiers utilitaires à la racine du module**
- **Fichier** : `diagnostic.py`, `cleanup_corrupted_passwords.py`, `fix_database.sql`, `install.sh`
- **Détail** : Des scripts de maintenance/diagnostic sont présents à la racine du module. Ces fichiers ne font pas partie d'un module Odoo standard et ne sont pas référencés dans le manifest.
- **Impact** : Livraison de scripts potentiellement sensibles dans le module. Le script `fix_database.sql` contient des requêtes SQL directes sur la base de données.
- **Action corrective** :
  - [ ] Déplacer ces fichiers dans un dossier `tools/` ou `scripts/` exclu du package de production, ou les supprimer si non nécessaires à la livraison.

**E — Présence d'un dossier `migrations/` pour la version 19.0.1.0.0**
- **Fichier** : `migrations/19.0.1.0.0/pre-migrate.py`
- **Détail** : Un script de migration est présent pour la version initiale (1.0.0). En principe, il n'y a pas de migration nécessaire lors de la première installation.
- **Impact** : Exécution potentiellement inutile lors de l'installation initiale.
- **Action corrective** :
  - [ ] Vérifier si ce script est réellement nécessaire pour la version initiale. Si non, le supprimer ou le documenter.

### 🔵 Informations

**E — Absence de README.md remplacé par README.rst**
- **Détail** : Le module disposait d'un `README.md`. La norme Odoo Apps recommande `README.rst`. Ce point a été corrigé lors de la mise en forme. Aucune action supplémentaire requise.

---

## Actions correctives — Récapitulatif

> Cocher les actions à exécuter, puis renvoyer ce fichier avec le module.

### 🟠 Importantes
- [ ] A05 — Documenter le `sudo()` dans `get_cipher()` pour la lecture/écriture de la clé (`models/password_entry.py:35,43`)
- [ ] A07 — Remplacer `except Exception` par `except (InvalidToken, ValueError)` dans `_compute_password` (`models/password_entry.py:93`)
- [ ] C03 — Valider avec le commanditaire l'accès total Manager et documenter la décision (`security/password_manager_security.xml`)
- [ ] D03 — Évaluer `store=True` sur `sharing_summary` si les performances liste sont insuffisantes (`models/password_entry.py`)

### 🟡 Mineures
- [ ] A12 — Envelopper les chaînes utilisateur dans `_()` pour la traduction (`models/password_entry.py` — multiples occurrences)
- [ ] B — Créer une action dédiée pour "Mes mots de passe" avec domain `[('create_uid','=',uid)]` (`views/password_entry_views.xml`)
- [ ] E — Déplacer `diagnostic.py`, `cleanup_corrupted_passwords.py`, `fix_database.sql`, `install.sh` hors du package de production
- [ ] E — Vérifier la nécessité du script de migration version 19.0.1.0.0 (`migrations/19.0.1.0.0/pre-migrate.py`)

### 🔵 Informations
- [ ] D03 — Évaluer les performances de `password` et `sharing_summary` (non stockés) sur des volumes importants
- [ ] E — Le `README.md` a été remplacé par un `README.rst` conforme à la norme Odoo Apps
