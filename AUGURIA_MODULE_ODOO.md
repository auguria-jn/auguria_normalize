# AUGURIA — Référentiel de mise à jour module Odoo

> **Usage** : Joindre ce fichier + le ZIP du module à mettre à jour.
> **Prompt** : `Met à jour le module joint`
> Ce fichier contient toutes les instructions nécessaires : charte graphique, règles de remise en forme, et consignes de livraison.

---

## Instructions pour Claude

Quand l'utilisateur demande de **mettre à jour un module** en joignant ce fichier et un ZIP :

1. **Décompresser** le ZIP et analyser l'intégralité du code source
2. **Appliquer toutes les règles** décrites ci-dessous (sections 1 à 6)
3. **Effectuer l'audit qualité** (section 7) et générer le fichier `controle_qualite.md` à la racine du module — **sans modifier le code source** pour cette étape
4. **Livrer** :
   - Le module complet repackagé en **ZIP** (contenant le `controle_qualite.md`)
   - Un **aperçu HTML** autonome de la page `index.html`
5. **Résumer** les modifications effectuées et les anomalies détectées

---

## 1. Identité Auguria

### Logo Auguria (pour le `index.html`)
- **Format** : PNG, 450×112 px
- **Intégration** : en base64 directement dans le HTML
- **Base64** : `data:image/png;base64,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`

### Couleurs

| Nom | HEX | Usage |
|-----|-----|-------|
| **Bleu Auguria** | `#185ADB` | Couleur principale — titres, bordures, en-têtes tableaux, encadrés |
| **Orange Auguria** | `#FFBA00` | Accent — barres, bordures gauche titres, badges, détails icône |
| Bleu foncé | `#0D2760` | Texte sombre, labels techniques, sous-titres |
| Gris texte | `#333333` | Corps de texte |
| Gris clair | `#F5F5F5` | Fonds de sections, encadrés techniques, pied de cartouche |
| Blanc | `#FFFFFF` | Fonds principaux |
| Vert validation | `#27AE60` | ✓ dans les tableaux de droits |
| Rouge refus | `#E74C3C` | ✗ dans les tableaux de droits |
| Bleu table hover | `#EEF2FB` | Survol lignes tableaux |
| Bleu table zebra | `#F9FAFE` | Lignes paires tableaux |
| Jaune transient fond | `#FFF3CD` | Badge "Transient" |
| Jaune transient texte | `#856404` | Badge "Transient" |

### Informations société
- **Auteur** : `AUGURIA by ANOR`
- **Site web** : `https://www.auguria.fr`
- **Raison sociale** : Auguria
- **Activité** : Consultant - Intégrateur Odoo — PME, ETI, grandes entreprises
- **Implantations** : Nantes, Paris
- **Licence par défaut** : LGPL-3

---

## 2. Nettoyage des fichiers XML

### Retours à la ligne
- Supprimer les lignes vides multiples consécutives (garder **1 seule ligne vide** max entre les blocs)
- Supprimer les lignes vides en début et fin de balise `<odoo>`, `<data>`, `<record>`, `<field name="arch">`
- Supprimer les espaces trailing en fin de ligne

### Indentation
- Indentation uniforme : **4 espaces** (pas de tabulations)
- Balises XML imbriquées : indentation cohérente
- Aligner les attributs longs sur plusieurs lignes si la ligne dépasse 120 caractères

### Structure
- Séparer chaque `<record>` par **1 ligne vide**
- Regrouper les records par type avec un commentaire de section :
```xml
<!-- ============================================================ -->
<!-- Form View                                                     -->
<!-- ============================================================ -->
```
- Chaque fichier XML commence par `<?xml version="1.0" encoding="utf-8"?>` suivi de `<odoo>`

---

## 3. Commentaires fonctionnels dans le code source

### En-tête de fichier Python (.py)
```python
# -*- coding: utf-8 -*-
# =============================================================================
# Module : nom_technique_module
# Fichier : nom_du_fichier.py
# Description : Description fonctionnelle du fichier (1-2 lignes)
# Auteur : AUGURIA by ANOR
# Création : YYYY-MM-DD
# Mise à jour : YYYY-MM-DD
# =============================================================================
```

### En-tête de fichier XML (.xml)
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
    Module : nom_technique_module
    Fichier : nom_du_fichier.xml
    Description : Description fonctionnelle du fichier
    Auteur : AUGURIA by ANOR
    Création : YYYY-MM-DD
    Mise à jour : YYYY-MM-DD
-->
<odoo>
```

### En-tête de fichier JavaScript (.js)
```javascript
/** @odoo-module **/
// =============================================================================
// Module : nom_technique_module
// Fichier : nom_du_fichier.js
// Description : Description fonctionnelle du fichier
// Auteur : AUGURIA by ANOR
// Création : YYYY-MM-DD
// Mise à jour : YYYY-MM-DD
// =============================================================================
```

### En-tête de fichier CSS (.css)
```css
/* =============================================================================
   Module : nom_technique_module
   Fichier : nom_du_fichier.css
   Description : Description fonctionnelle du fichier
   Auteur : AUGURIA by ANOR
   Création : YYYY-MM-DD
   Mise à jour : YYYY-MM-DD
   ============================================================================= */
```

### Commentaires Python

#### Classes
```python
class MonModele(models.Model):
    """
    Modèle : mon.modele
    Rôle fonctionnel : Gère les [objet métier] pour [contexte].
    Héritage : [mail.thread, etc.] si applicable
    """
```

#### Champs — commenter uniquement ceux dont la logique métier n'est pas évidente
```python
# Montant HT recalculé automatiquement à chaque ajout de ligne de commande
amount_untaxed = fields.Monetary(...)
```

#### Méthodes — décrire le **pourquoi fonctionnel**, pas le comment technique
```python
def action_validate(self):
    """
    Valide le document et déclenche :
    - Génération du numéro de séquence
    - Notification aux responsables
    - Verrouillage de l'édition
    Appelé depuis : bouton "Valider" du formulaire
    """
```

#### Sections dans les classes
```python
    # -------------------------------------------------------------------------
    # Champs
    # -------------------------------------------------------------------------

    # -------------------------------------------------------------------------
    # Contraintes
    # -------------------------------------------------------------------------

    # -------------------------------------------------------------------------
    # CRUD
    # -------------------------------------------------------------------------

    # -------------------------------------------------------------------------
    # Actions métier
    # -------------------------------------------------------------------------

    # -------------------------------------------------------------------------
    # Méthodes de calcul
    # -------------------------------------------------------------------------
```

### Commentaires XML
```xml
<!-- Vue formulaire : saisie/consultation d'un [objet métier] -->
<!-- Séquence de numérotation : format [PREFIX]/YYYY/NNNN -->
```

### Dates
- **Création / Mise à jour** : date du jour de la remise en forme (`YYYY-MM-DD`)
- Si un historique git ou changelog existe, utiliser les dates réelles

---

## 4. Mise en forme des fichiers descriptifs

### `__manifest__.py`
- **author** : `'AUGURIA by ANOR'`
- **website** : `'https://www.auguria.fr'`
- **license** : `'LGPL-3'` (sauf indication contraire)
- **version** : format `<odoo_version>.<major>.<minor>.<patch>` (ex: `17.0.1.0.0`)
- **category** : catégorie Odoo appropriée au rôle du module
- **summary** : description courte en français (max 80 caractères)
- **description** : 3-5 lignes décrivant le rôle fonctionnel
- **depends** : vérifier que toutes les dépendances réelles sont listées
- **data** : tous les fichiers XML référencés, dans l'ordre : `security/ → data/ → views/*_views.xml → views/menu.xml → wizard/ → report/`

### `README.rst`
- **Titre** : nom lisible du module
- **Description** : rôle fonctionnel (3-5 lignes)
- **Installation** : prérequis éventuels
- **Configuration** : paramètres à configurer après installation
- **Usage** : parcours utilisateur
- **Auteurs / Maintainers** : AUGURIA by ANOR

### `static/description/index.html`
Appliquer le gabarit cartouche industriel Auguria (voir section 6 pour le gabarit complet) :
- **Cartouche en-tête** : logo Auguria base64, nom du module, description, version/licence/auteur/catégorie
- **Section Description** : résumé fonctionnel
- **Section Fonctionnalités** : liste extraite du code
- **Section Dépendances** : badges des modules requis (extraits de `depends`)
- **Section Technique** : tableaux des vues, groupes de sécurité avec matrice CRUD, modèles de données
- **Pied de cartouche** : informations Auguria

---

## 5. Icônes du module

Le module utilise **deux icônes distinctes** avec des rôles différents :

### 5.1 Icône du module — `static/description/icon.png`

C'est l'icône affichée sur l'**Odoo Apps Store** et dans la liste des applications (menu Apps). Elle porte l'**identité Auguria** et reste identique pour tous les modules.

- **Contenu** : logo G condensé Auguria (orange `#FFBA00` sur fond transparent ou blanc)
- **Format** : PNG, `128×128 px`
- **Source** : fourni dans les assets Auguria ou généré avec Pillow :
```python
from PIL import Image, ImageDraw, ImageFont

SIZE = 128
img = Image.new('RGBA', (SIZE, SIZE), (0, 0, 0, 0))
draw = ImageDraw.Draw(img)
draw.rounded_rectangle([0, 0, SIZE-1, SIZE-1], radius=26, fill='#FFFFFF')
# Dessiner le G stylisé en orange #FFBA00
img.save('static/description/icon.png')
```
- **Règle** : ne jamais remplacer ce fichier par une icône thématique — il représente la marque Auguria

### 5.2 Icône du menu — `static/description/menu_icon.png`

C'est l'icône affichée dans la **barre de navigation Odoo** (menu applicatif en haut). Elle est **unique à chaque module** et représente visuellement son rôle fonctionnel.

#### Analyse
Avant de générer l'icône, identifier le **domaine fonctionnel** du module :
- Lire le `__manifest__.py` : `name`, `summary`, `category`, `depends`
- Lire les noms de modèles (`_name`, `_description`) dans les fichiers Python
- Identifier le domaine métier

#### Design
Générer `static/description/menu_icon.png` — PNG `128×128 px` :

- **Fond** : Bleu Auguria `#185ADB`, coins arrondis (~20%)
- **Pictogramme** : blanc `#FFFFFF`, centré, représentatif du rôle :
  - Ventes / CRM → panier, graphique, poignée de main
  - Stock / Inventaire → carton, entrepôt, palette
  - Comptabilité / Finance → calculatrice, pièce, balance
  - RH / Employés → personne, groupe, badge
  - Helpdesk / Support → casque, ticket, bulle
  - Fabrication → engrenage, usine, chaîne
  - Qualité → check, étoile, bouclier
  - Planning / Projet → calendrier, horloge
  - Documents / Rapport → fichier, classeur
  - Configuration / Technique → clé à molette
- **Accent** : un élément en Orange `#FFBA00` (contour, détail, badge, bande)
- **Style** : flat design, lignes épurées, sans texte, lisible en 30px

#### Méthode de génération (Pillow)
```python
from PIL import Image, ImageDraw

SIZE = 128
RADIUS = 26
BLUE = '#185ADB'
ORANGE = '#FFBA00'
WHITE = '#FFFFFF'

img = Image.new('RGBA', (SIZE, SIZE), (0, 0, 0, 0))
draw = ImageDraw.Draw(img)
draw.rounded_rectangle([0, 0, SIZE-1, SIZE-1], radius=RADIUS, fill=BLUE)
# Accent orange + pictogramme blanc à adapter selon le rôle du module
img.save('static/description/menu_icon.png')
```

### 5.3 Attribut `web_icon` sur le menu root
Le `web_icon` doit pointer vers l'**icône du menu** (pas l'icône du module) :
```xml
<menuitem id="nom_module_menu_root"
          name="Nom du Module"
          web_icon="nom_module,static/description/menu_icon.png"
          .../>
```
- Si absent : l'ajouter
- Si `web_icon` pointe vers `icon.png` : le corriger vers `menu_icon.png`
- Module d'héritage sans menu root propre : générer `menu_icon.png` quand même (pour le store), pas de `web_icon` à modifier

---

## 6. Gabarit `index.html` complet

```html
<section class="oe_container">
    <div class="oe_row oe_spaced">

        <!-- CARTOUCHE EN-TÊTE INDUSTRIEL -->
        <div style="
            border: 3px solid #185ADB;
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 32px;
            box-shadow: 0 2px 8px rgba(13, 39, 96, 0.10);
        ">
            <div style="background: #FFBA00; height: 6px; width: 100%;"></div>
            <div style="display: flex; align-items: stretch; min-height: 90px;">

                <!-- Logo Auguria (base64 de la section 1) -->
                <div style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    padding: 12px 24px;
                    border-right: 2px solid #185ADB;
                    background: #FFFFFF;
                    min-width: 180px;
                ">
                    <img src="data:image/png;base64,{LOGO_BASE64}" alt="Auguria" style="max-height: 52px;" />
                </div>

                <!-- Titre du module -->
                <div style="
                    flex: 1;
                    display: flex;
                    flex-direction: column;
                    justify-content: center;
                    padding: 12px 24px;
                    background: #FFFFFF;
                    border-right: 2px solid #185ADB;
                ">
                    <div style="font-size: 10px; font-weight: 600; color: #FFBA00; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 4px;">Module Odoo</div>
                    <div style="font-size: 22px; font-weight: 700; color: #185ADB; line-height: 1.2;">NOM DU MODULE</div>
                    <div style="font-size: 12px; color: #333333; margin-top: 4px;">Description courte</div>
                </div>

                <!-- Infos techniques -->
                <div style="
                    display: flex;
                    flex-direction: column;
                    justify-content: center;
                    padding: 10px 20px;
                    background: #F5F5F5;
                    min-width: 200px;
                    font-size: 11px;
                    color: #333333;
                    line-height: 1.8;
                ">
                    <div><span style="font-weight: 700; color: #0D2760;">Version :</span> 17.0.1.0.0</div>
                    <div><span style="font-weight: 700; color: #0D2760;">Licence :</span> LGPL-3</div>
                    <div><span style="font-weight: 700; color: #0D2760;">Auteur :</span> AUGURIA by ANOR</div>
                    <div><span style="font-weight: 700; color: #0D2760;">Catégorie :</span> Catégorie</div>
                </div>

            </div>
            <div style="background: #FFBA00; height: 6px; width: 100%;"></div>
        </div>

        <!-- DESCRIPTION -->
        <div style="margin-bottom: 28px;">
            <h2 style="color: #185ADB; font-size: 18px; font-weight: 700; border-left: 4px solid #FFBA00; padding-left: 12px; margin-bottom: 12px;">Description</h2>
            <p style="color: #333333; font-size: 13px; line-height: 1.7; padding-left: 16px;">
                Description détaillée du module.
            </p>
        </div>

        <!-- FONCTIONNALITÉS -->
        <div style="margin-bottom: 28px;">
            <h2 style="color: #185ADB; font-size: 18px; font-weight: 700; border-left: 4px solid #FFBA00; padding-left: 12px; margin-bottom: 12px;">Fonctionnalités</h2>
            <ul style="color: #333333; font-size: 13px; line-height: 2; padding-left: 32px;">
                <li>Fonctionnalité 1</li>
            </ul>
        </div>

        <!-- ============================================================ -->
        <!-- DÉPENDANCES                                                   -->
        <!-- ============================================================ -->
        <div style="margin-bottom: 28px;">
            <h2 style="color: #185ADB; font-size: 18px; font-weight: 700; border-left: 4px solid #FFBA00; padding-left: 12px; margin-bottom: 16px;">Dépendances</h2>

            <!-- Modules requis -->
            <div style="margin-bottom: 16px; padding-left: 16px;">
                <div style="font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block;">Modules Odoo requis</div>
                <p style="color: #333333; font-size: 12px; line-height: 1.7; margin-bottom: 12px;">
                    Ce module nécessite l'installation préalable des modules suivants :
                </p>
                <div>
                    <span style="display: inline-block; background: #185ADB; color: #FFFFFF; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px; margin: 4px 4px 4px 0;">base</span>
                </div>
            </div>

            <!-- Modules optionnels -->
            <div style="padding-left: 16px;">
                <div style="font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block;">Modules optionnels</div>
                <p style="color: #999999; font-size: 12px; font-style: italic;">Aucun module optionnel requis.</p>
            </div>
        </div>

        <!-- ============================================================ -->
        <!-- INFORMATIONS TECHNIQUES                                       -->
        <!-- ============================================================ -->
        <div style="margin-bottom: 28px;">
            <h2 style="color: #185ADB; font-size: 18px; font-weight: 700; border-left: 4px solid #FFBA00; padding-left: 12px; margin-bottom: 16px;">Informations techniques</h2>

            <!-- Vues impactées -->
            <div style="margin-bottom: 20px; padding-left: 16px;">
                <div style="font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block;">Vues impactées</div>
                <table style="width: 100%; border-collapse: collapse; font-size: 12px; color: #333333;">
                    <thead>
                        <tr>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 4px 0 0 0;">Vue</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">Type</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 0 4px 0 0;">Modèle</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><code style="background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760;">xml_id</code></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;">Type</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><code style="background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760;">model.name</code></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Groupes de sécurité & Droits -->
            <div style="margin-bottom: 20px; padding-left: 16px;">
                <div style="font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block;">Groupes de sécurité &amp; Droits</div>
                <table style="width: 100%; border-collapse: collapse; font-size: 12px; color: #333333;">
                    <thead>
                        <tr>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 4px 0 0 0;">Groupe</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">XML ID</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: center; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">Lecture</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: center; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">Écriture</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: center; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">Création</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: center; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 0 4px 0 0;">Suppression</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><span style="display: inline-block; background: #FFFFFF; color: #185ADB; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px; border: 2px solid #185ADB;">Utilisateur</span></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><code style="background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760;">group_xml_id</code></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #E74C3C; font-weight: 700; text-align: center;">&#10007;</td>
                        </tr>
                        <tr style="background: #F9FAFE;">
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><span style="display: inline-block; background: #185ADB; color: #FFFFFF; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px;">Manager</span></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><code style="background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760;">group_xml_id</code></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5; color: #27AE60; font-weight: 700; text-align: center;">&#10003;</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Modèles de données -->
            <div style="padding-left: 16px;">
                <div style="font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block;">Modèles de données</div>
                <table style="width: 100%; border-collapse: collapse; font-size: 12px; color: #333333;">
                    <thead>
                        <tr>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 4px 0 0 0;">Modèle</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px;">Description</th>
                            <th style="background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; border-radius: 0 4px 0 0;">Type</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><code style="background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760;">model.name</code></td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;">Description</td>
                            <td style="padding: 8px 12px; border-bottom: 1px solid #E8ECF5;"><span style="display: inline-block; background: #FFFFFF; color: #185ADB; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px; border: 2px solid #185ADB;">Persistant</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- PIED DE CARTOUCHE -->
        <div style="border: 2px solid #185ADB; border-radius: 4px; overflow: hidden; margin-top: 32px;">
            <div style="background: #FFBA00; height: 4px; width: 100%;"></div>
            <div style="display: flex; justify-content: space-between; align-items: center; padding: 10px 24px; background: #F5F5F5; font-size: 11px; color: #333333;">
                <div><span style="font-weight: 700; color: #0D2760;">Auguria</span> — Consultant &amp; Intégrateur Odoo — Nantes &amp; Paris</div>
                <div><a href="https://www.auguria.fr" style="color: #185ADB; font-weight: 600; text-decoration: none;">Auguria.fr</a></div>
            </div>
            <div style="background: #FFBA00; height: 4px; width: 100%;"></div>
        </div>

    </div>
</section>
```

> **Note** : Remplacer `{LOGO_BASE64}` par la chaîne base64 complète du logo Auguria fournie dans la section 1. Remplir tous les contenus (nom, description, dépendances, vues, groupes, modèles) à partir de l'analyse du code source du module. Le gabarit utilise exclusivement des **styles inline** pour garantir un rendu correct dans Odoo (apps.odoo.com et back-office). Aucune balise `<style>`, `<script>`, ni class CSS externe.

---

## 7. Audit qualité — `controle_qualite.md`

### Principe
L'audit qualité est une étape d'**observation uniquement**. Il ne modifie **aucun fichier** du module. Son résultat est un fichier `controle_qualite.md` placé à la racine du module, qui :
- Liste toutes les anomalies détectées, classées par gravité
- Propose des **actions correctives sous forme de cases à cocher**
- Peut être renvoyé ultérieurement avec le module pour demander l'exécution des corrections cochées

### Niveaux de gravité

| Icône | Niveau | Signification |
|-------|--------|---------------|
| 🔴 | **Critique** | Risque de bug, faille de sécurité, crash potentiel |
| 🟠 | **Important** | Mauvaise pratique ayant un impact sur la performance ou la maintenabilité |
| 🟡 | **Mineur** | Convention non respectée, amélioration recommandée |
| 🔵 | **Info** | Suggestion d'optimisation, point d'attention |

### Contrôles à effectuer

#### A. Qualité du code Python

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

#### B. Qualité des fichiers XML

| # | Contrôle | Gravité |
|---|----------|---------|
| B01 | Records en double (même `id` dans plusieurs fichiers) | 🔴 |
| B02 | Vues héritées ciblant des XPath inexistants ou fragiles | 🟠 |
| B03 | Groupes de sécurité référencés mais non définis | 🔴 |
| B04 | Actions window pointant vers des modèles inexistants | 🔴 |
| B05 | Champs référencés dans les vues mais absents du modèle Python | 🔴 |
| B06 | Fichiers XML listés dans le manifest mais absents du dossier | 🔴 |
| B07 | Fichiers XML présents dans le dossier mais non listés dans le manifest | 🟠 |

#### C. Sécurité & droits d'accès

| # | Contrôle | Gravité |
|---|----------|---------|
| C01 | Modèles sans règle d'accès dans `ir.model.access.csv` | 🔴 |
| C02 | Modèles `TransientModel` sans restriction d'accès | 🟠 |
| C03 | Record rules trop permissives (domain `[(1,'=',1)]`) | 🟠 |
| C04 | Groupes de sécurité sans hiérarchie cohérente (manager n'implique pas user) | 🟡 |

#### D. Performance

| # | Contrôle | Gravité |
|---|----------|---------|
| D01 | `.search()` ou `.browse()` dans une boucle sans prefetch | 🟠 |
| D02 | `.write()` appelé enregistrement par enregistrement au lieu d'un batch | 🟠 |
| D03 | Champs `compute` non stockés déclenchant des calculs à chaque lecture | 🟡 |
| D04 | `_compute` faisant un `.search()` sans limite sur tables volumineuses | 🟠 |
| D05 | Absence de `_order` sur les modèles fréquemment listés | 🟡 |

#### E. Architecture & bonnes pratiques Odoo

| # | Contrôle | Gravité |
|---|----------|---------|
| E01 | Logique métier dans un contrôleur au lieu du modèle | 🟠 |
| E02 | Wizard qui modifie directement des données au lieu de passer par le modèle | 🟡 |
| E03 | Données de démo mélangées avec les données de production | 🟡 |
| E04 | `_name` différent de `_table` sans raison documentée | 🟡 |
| E05 | Absence de `_description` sur les modèles | 🟡 |
| E06 | Champs `Selection` avec valeurs en dur là où un modèle séparé serait plus maintenable | 🔵 |
| E07 | Absence de `_rec_name` quand le champ `name` n'existe pas | 🟠 |

### Gabarit du fichier `controle_qualite.md`

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

### Règles de rédaction du rapport

1. **Chaque anomalie** doit indiquer : le code du contrôle, le fichier et la ligne approximative, un détail concret, l'impact, et une action corrective en case à cocher
2. **Les contrôles conformes** sont listés brièvement pour montrer qu'ils ont été vérifiés (pas juste omis)
3. **Le récapitulatif final** regroupe toutes les cases à cocher de tout le document, classées par gravité, avec la référence fichier:ligne — c'est cette section qui sera utilisée pour lancer les corrections
4. **Si aucune anomalie** n'est détectée dans une catégorie, indiquer "Aucune anomalie détectée" sous le niveau de gravité
5. **Ne jamais inventer** d'anomalie : si le code est propre, le rapport le reflète
6. **Sections vides** : supprimer les sous-sections de gravité qui n'ont aucune anomalie (ne garder que celles qui contiennent des résultats)

### Utilisation ultérieure du rapport

Quand l'utilisateur renvoie le fichier `controle_qualite.md` avec des cases cochées et le ZIP du module, avec un prompt du type `Applique les corrections cochées` :
1. Lire les cases cochées (`- [x]`)
2. Appliquer **uniquement** les corrections correspondantes sur le code source
3. Mettre à jour les dates de mise à jour dans les en-têtes des fichiers modifiés
4. Régénérer le `controle_qualite.md` pour refléter les corrections appliquées
5. Livrer le module corrigé en ZIP et le rapport controle_qualite.md indépendemment

---

## 8. Checklist de validation

Avant de livrer le module repackagé, vérifier :

- [ ] Aucune ligne vide multiple consécutive dans les XML
- [ ] Indentation uniforme 4 espaces dans tous les fichiers
- [ ] En-tête AUGURIA présent dans chaque fichier source (.py, .xml, .js, .css)
- [ ] Commentaires fonctionnels sur les classes, méthodes non triviales, et champs à logique métier
- [ ] Sections séparées par des commentaires dans les classes Python
- [ ] `__manifest__.py` complet (auteur, site web, version, catégorie, summary, description)
- [ ] `README.rst` rédigé avec le contenu fonctionnel du module
- [ ] `index.html` conforme au gabarit cartouche Auguria avec sections techniques remplies
- [ ] `icon.png` = logo G condensé Auguria (128×128, identité marque, identique pour tous les modules)
- [ ] `menu_icon.png` générée (128×128, fond bleu, pictogramme blanc, accent orange, spécifique au rôle du module)
- [ ] `web_icon` du menu root pointe vers `menu_icon.png` (pas `icon.png`)
- [ ] Fichiers `data` dans le manifest listés dans le bon ordre
- [ ] Pas d'import inutilisé dans les fichiers Python
- [ ] Encodage UTF-8 sur tous les fichiers
- [ ] `controle_qualite.md` généré à la racine du module avec tous les contrôles (A01–E07)
- [ ] Récapitulatif des actions correctives avec cases à cocher en fin de rapport

---

*Version : 3.2 — Mars 2026*
