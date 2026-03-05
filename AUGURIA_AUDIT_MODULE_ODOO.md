# AUGURIA — Audit qualité module Odoo

> **Usage** : Joindre ce fichier + le ZIP du module à auditer.
> **Prompt** : `Audite le module joint`
> Ce fichier génère un rapport de contrôle qualité **sans modifier aucun fichier** du module.

---

## Instructions pour Claude

Quand l'utilisateur demande d'**auditer un module** en joignant ce fichier et un ZIP :

1. **Décompresser** le ZIP et analyser l'intégralité du code source
2. **Exécuter tous les contrôles** décrits ci-dessous (catégories A à E, 30 points de contrôle)
3. **Générer** le fichier `controle_qualite.md` selon le gabarit (section 3)
4. **Livrer** :
   - Le fichier `controle_qualite.md` en téléchargement indépendant
   - Un résumé des anomalies détectées dans le message
5. **Ne modifier aucun fichier** du module — cet audit est uniquement un rapport d'observation

### Utilisation ultérieure du rapport

Quand l'utilisateur renvoie le fichier `controle_qualite.md` avec des cases cochées et le ZIP du module, avec un prompt du type `Applique les corrections cochées` :
1. Lire les cases cochées (`- [x]`)
2. Appliquer **uniquement** les corrections correspondantes sur le code source
3. Mettre à jour les dates de mise à jour dans les en-têtes des fichiers modifiés
4. Régénérer le `controle_qualite.md` pour refléter les corrections appliquées
5. Livrer le module corrigé en ZIP et le fichier `controle_qualite.md` indépendamment

---

## 1. Niveaux de gravité

| Icône | Niveau | Signification |
|-------|--------|---------------|
| 🔴 | **Critique** | Risque de bug, faille de sécurité, crash potentiel |
| 🟠 | **Important** | Mauvaise pratique ayant un impact sur la performance ou la maintenabilité |
| 🟡 | **Mineur** | Convention non respectée, amélioration recommandée |
| 🔵 | **Info** | Suggestion d'optimisation, point d'attention |

---

## 2. Contrôles à effectuer

### A. Qualité du code Python

| # | Contrôle | Gravité |
|---|----------|---------|
| A01 | Imports inutilisés ou manquants | 🟡 |
| A02 | Variables / champs déclarés mais jamais utilisés | 🟡 |
| A03 | Méthodes dupliquées ou quasi-identiques entre fichiers (copier-coller) | 🟠 |
| A04 | Méthodes trop longues (> 50 lignes) nécessitant un refactoring | 🟠 |
| A05 | Utilisation de `sudo()` injustifié (élévation de privilèges) | 🔴 |
| A06 | Appels SQL bruts (`self.env.cr.execute`) sans paramétrage (injection SQL) | 🔴 |
| A07 | `try/except` trop larges (catch `Exception` sans raison spécifique) | 🟠 |
| A08 | `.search()` dans une boucle `for` (problème de performance N+1) | 🟠 |
| A09 | Champs `compute` sans `depends` ou avec `depends` incorrects | 🔴 |
| A10 | `api.onchange` utilisé là où un `compute` serait plus adapté | 🟡 |
| A11 | Héritage de modèle (`_inherit`) sans ajout de valeur réel | 🟡 |
| A12 | Chaînes non wrappées dans `_()` (traductions manquantes) | 🟡 |

### B. Qualité des fichiers XML

| # | Contrôle | Gravité |
|---|----------|---------|
| B01 | Records en double (même `id` dans plusieurs fichiers) | 🔴 |
| B02 | Vues héritées ciblant des XPath inexistants ou fragiles | 🟠 |
| B03 | Groupes de sécurité référencés mais non définis | 🔴 |
| B04 | Actions window pointant vers des modèles inexistants | 🔴 |
| B05 | Champs référencés dans les vues mais absents du modèle Python | 🔴 |
| B06 | Fichiers XML listés dans le manifest mais absents du dossier | 🔴 |
| B07 | Fichiers XML présents dans le dossier mais non listés dans le manifest | 🟠 |

### C. Sécurité & droits d'accès

| # | Contrôle | Gravité |
|---|----------|---------|
| C01 | Modèles sans règle d'accès dans `ir.model.access.csv` | 🔴 |
| C02 | Modèles `TransientModel` sans restriction d'accès | 🟠 |
| C03 | Record rules trop permissives (domain `[(1,'=',1)]`) | 🟠 |
| C04 | Groupes de sécurité sans hiérarchie cohérente (manager n'implique pas user) | 🟡 |

### D. Performance

| # | Contrôle | Gravité |
|---|----------|---------|
| D01 | `.search()` ou `.browse()` dans une boucle sans prefetch | 🟠 |
| D02 | `.write()` appelé enregistrement par enregistrement au lieu d'un batch | 🟠 |
| D03 | Champs `compute` non stockés déclenchant des calculs à chaque lecture | 🟡 |
| D04 | `_compute` faisant un `.search()` sans limite sur tables volumineuses | 🟠 |
| D05 | Absence de `_order` sur les modèles fréquemment listés | 🟡 |

### E. Architecture & bonnes pratiques Odoo

| # | Contrôle | Gravité |
|---|----------|---------|
| E01 | Logique métier dans un contrôleur au lieu du modèle | 🟠 |
| E02 | Wizard qui modifie directement des données au lieu de passer par le modèle | 🟡 |
| E03 | Données de démo mélangées avec les données de production | 🟡 |
| E04 | `_name` différent de `_table` sans raison documentée | 🟡 |
| E05 | Absence de `_description` sur les modèles | 🟡 |
| E06 | Champs `Selection` avec valeurs en dur là où un modèle séparé serait plus maintenable | 🔵 |
| E07 | Absence de `_rec_name` quand le champ `name` n'existe pas | 🟠 |

---

## 3. Gabarit du fichier `controle_qualite.md`

Le fichier généré doit suivre **exactement** cette structure :

```markdown
# Contrôle Qualité — {nom_technique_module}

> **Module** : {nom_lisible}
> **Version** : {version}
> **Date d'audit** : {YYYY-MM-DD}
> **Auditeur** : Claude (AUGURIA by ANOR)
>
> ⚠️ **Ce fichier est un rapport d'observation. Aucune modification n'a été apportée au code.**
> Pour lancer les corrections, cocher les actions souhaitées et renvoyer ce fichier avec le module en demandant : `Applique les corrections cochées`

---

## Synthèse

| Niveau | Nombre |
|--------|--------|
| 🔴 Critique | {n} |
| 🟠 Important | {n} |
| 🟡 Mineur | {n} |
| 🔵 Info | {n} |
| ✅ Conforme | {n} contrôles passés sans anomalie |

---

## A. Qualité du code Python

### ✅ Contrôles conformes
<!-- Lister ici les contrôles passés sans anomalie, ex: -->
<!-- - A01 — Imports : aucun import inutilisé détecté -->

### 🔴 Anomalies critiques
<!-- Pour chaque anomalie critique détectée : -->

**A09 — Champ compute sans depends**
- **Fichier** : `models/mon_modele.py`, ligne ~42
- **Détail** : Le champ `amount_total` est un compute sans décorateur `@api.depends`
- **Impact** : Le champ ne sera jamais recalculé automatiquement
- **Action corrective** :
  - [ ] Ajouter `@api.depends('line_ids.price_subtotal')` sur la méthode `_compute_amount_total`

### 🟠 Anomalies importantes
<!-- Même format que ci-dessus -->

**A08 — Search dans une boucle**
- **Fichier** : `models/mon_modele.py`, ligne ~78
- **Détail** : `self.env['product.product'].search(...)` appelé dans un `for record in self`
- **Impact** : Requête SQL exécutée N fois au lieu d'une seule
- **Action corrective** :
  - [ ] Refactorer en un seul `.search()` avant la boucle avec un dictionnaire de lookup

### 🟡 Anomalies mineures
<!-- Même format -->

### 🔵 Informations
<!-- Même format -->

---

## B. Qualité des fichiers XML

### ✅ Contrôles conformes
### 🔴 Anomalies critiques
### 🟠 Anomalies importantes
### 🟡 Anomalies mineures

---

## C. Sécurité & droits d'accès

### ✅ Contrôles conformes
### 🔴 Anomalies critiques
### 🟠 Anomalies importantes
### 🟡 Anomalies mineures

---

## D. Performance

### ✅ Contrôles conformes
### 🟠 Anomalies importantes
### 🟡 Anomalies mineures
### 🔵 Informations

---

## E. Architecture & bonnes pratiques Odoo

### ✅ Contrôles conformes
### 🟠 Anomalies importantes
### 🟡 Anomalies mineures
### 🔵 Informations

---

## Actions correctives — Récapitulatif

> Cocher les actions à exécuter, puis renvoyer ce fichier avec le module.

### 🔴 Critiques
- [ ] A09 — Ajouter `@api.depends(...)` sur `_compute_amount_total` (`models/mon_modele.py:42`)
- [ ] ...

### 🟠 Importantes
- [ ] A08 — Refactorer le `.search()` en boucle (`models/mon_modele.py:78`)
- [ ] ...

### 🟡 Mineures
- [ ] A01 — Supprimer l'import inutilisé `from odoo.exceptions import UserError` (`models/mon_modele.py:3`)
- [ ] ...

### 🔵 Informations
- [ ] E06 — Envisager un modèle séparé pour les valeurs du champ Selection `state`
- [ ] ...
```

---

## 4. Règles de rédaction du rapport

1. **Chaque anomalie** doit indiquer : le code du contrôle, le fichier et la ligne approximative, un détail concret, l'impact, et une action corrective en case à cocher
2. **Les contrôles conformes** sont listés brièvement pour montrer qu'ils ont été vérifiés (pas juste omis)
3. **Le récapitulatif final** regroupe toutes les cases à cocher de tout le document, classées par gravité, avec la référence fichier:ligne — c'est cette section qui sera utilisée pour lancer les corrections
4. **Si aucune anomalie** n'est détectée dans une catégorie, indiquer "Aucune anomalie détectée" sous le niveau de gravité
5. **Ne jamais inventer** d'anomalie : si le code est propre, le rapport le reflète
6. **Sections vides** : supprimer les sous-sections de gravité qui n'ont aucune anomalie (ne garder que celles qui contiennent des résultats)

---

*Version : 1.0 — Mars 2026*
