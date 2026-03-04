# AUGURIA — Référentiel de mise à jour module Odoo

> **Usage** : Joindre ce fichier + le ZIP du module à mettre à jour.
> **Prompt** : `Met à jour le module joint`
> Ce fichier contient toutes les instructions nécessaires : charte graphique, règles de remise en forme, et consignes de livraison.

---

## Instructions pour Claude

Quand l'utilisateur demande de **mettre à jour un module** en joignant ce fichier et un ZIP :

1. **Décompresser** le ZIP et analyser l'intégralité du code source
2. **Appliquer toutes les règles** décrites ci-dessous (sections 1 à 7)
3. **Livrer** :
   - Le module complet repackagé en **ZIP**
   - Un **aperçu HTML** autonome de la page `index.html`
4. **Résumer** les modifications effectuées

---

## 1. Identité Auguria

### Logo Auguria (pour le `index.html`)
- **Format** : PNG, 450×112 px
- **Intégration** : en base64 directement dans le HTML
- **Base64** : `data:image/png;base64,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`

### Couleurs

| Nom | HEX | Usage |
|-----|-----|-------|
| **Bleu Auguria** | `#185ADB` | Couleur principale — titres, bordures, onglets actifs, en-têtes tableaux |
| **Orange Auguria** | `#FFBA00` | Accent — barres, bordures gauche titres, badges, détails icône |
| Bleu foncé | `#0D2760` | Texte sombre, labels techniques, sous-titres |
| Gris texte | `#333333` | Corps de texte |
| Gris clair | `#F5F5F5` | Fonds de sections, onglets inactifs, pied de cartouche |
| Blanc | `#FFFFFF` | Fonds principaux |
| Vert validation | `#27AE60` | ✓ dans les tableaux de droits |
| Rouge refus | `#E74C3C` | ✗ dans les tableaux de droits |
| Bleu table hover | `#EEF2FB` | Survol lignes tableaux |
| Bleu table zebra | `#F9FAFE` | Lignes paires tableaux |
| Jaune transient fond | `#FFF3CD` | Badge "Transient" |
| Jaune transient texte | `#856404` | Badge "Transient" |

### Informations société
- **Auteur** : `AUDURIA by ANOR`
- **Site web** : `https://auduria.fr`
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
# Auteur : AUDURIA by ANOR
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
    Auteur : AUDURIA by ANOR
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
// Auteur : AUDURIA by ANOR
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
   Auteur : AUDURIA by ANOR
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
- **author** : `'AUDURIA by ANOR'`
- **website** : `'https://auduria.fr'`
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
- **Auteurs / Maintainers** : AUDURIA by ANOR

### `static/description/index.html`
Appliquer le gabarit cartouche industriel Auguria (voir section 6 pour le gabarit complet) :
- **Cartouche en-tête** : logo Auguria base64, nom du module, description, version/licence/auteur/catégorie
- **Section Description** : résumé fonctionnel
- **Section Fonctionnalités** : liste extraite du code
- **Onglet Dépendances** : badges des modules requis (extraits de `depends`)
- **Onglet Technique** : tableaux des vues, groupes de sécurité avec matrice CRUD, modèles de données
- **Pied de cartouche** : informations Auguria

---

## 5. Génération automatique de l'icône du module

### Analyse
Avant de générer l'icône, identifier le **domaine fonctionnel** du module :
- Lire le `__manifest__.py` : `name`, `summary`, `category`, `depends`
- Lire les noms de modèles (`_name`, `_description`) dans les fichiers Python
- Identifier le domaine métier

### Design de l'icône
Générer `static/description/icon.png` — PNG `128×128 px` :

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

### Méthode de génération (Pillow)
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
img.save('static/description/icon.png')
```

### Attribut `web_icon`
Vérifier que le menu root possède :
```xml
<menuitem id="nom_module_menu_root"
          name="Nom du Module"
          web_icon="nom_module,static/description/icon.png"
          .../>
```
- Si absent : l'ajouter
- Si incorrect : le corriger
- Module d'héritage sans menu root propre : générer l'icône quand même, pas de `web_icon` à modifier

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
                    <div><span style="font-weight: 700; color: #0D2760;">Auteur :</span> AUDURIA by ANOR</div>
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

        <!-- ONGLETS CSS PUR -->
        <style>
            .aug-tabs { margin-bottom: 28px; }
            .aug-tabs input[type="radio"] { display: none; }
            .aug-tabs .aug-tab-labels { display: flex; border-bottom: 3px solid #185ADB; margin-bottom: 0; }
            .aug-tabs .aug-tab-labels label { padding: 10px 24px; font-size: 13px; font-weight: 700; color: #0D2760; cursor: pointer; border: 2px solid transparent; border-bottom: none; border-radius: 6px 6px 0 0; margin-right: 4px; background: #F5F5F5; transition: background 0.2s, color 0.2s; user-select: none; }
            .aug-tabs .aug-tab-labels label:hover { background: #E8ECF5; }
            .aug-tabs .aug-tab-panel { display: none; padding: 20px 16px; border: 2px solid #185ADB; border-top: none; border-radius: 0 0 6px 6px; background: #FFFFFF; }
            .aug-tabs #aug-tab1:checked ~ .aug-tab-labels label[for="aug-tab1"],
            .aug-tabs #aug-tab2:checked ~ .aug-tab-labels label[for="aug-tab2"] { background: #185ADB; color: #FFFFFF; border-color: #185ADB; }
            .aug-tabs #aug-tab1:checked ~ .aug-panel-1,
            .aug-tabs #aug-tab2:checked ~ .aug-panel-2 { display: block; }
            .aug-badge { display: inline-block; background: #185ADB; color: #FFFFFF; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px; margin: 4px 4px 4px 0; }
            .aug-badge-outline { display: inline-block; background: #FFFFFF; color: #185ADB; font-size: 12px; font-weight: 600; padding: 4px 14px; border-radius: 3px; border: 2px solid #185ADB; margin: 4px 4px 4px 0; }
            .aug-tech-section { margin-bottom: 18px; }
            .aug-tech-title { font-size: 14px; font-weight: 700; color: #0D2760; margin-bottom: 8px; padding-bottom: 4px; border-bottom: 2px solid #FFBA00; display: inline-block; }
            .aug-tech-table { width: 100%; border-collapse: collapse; font-size: 12px; color: #333333; }
            .aug-tech-table thead th { background: #185ADB; color: #FFFFFF; font-weight: 600; padding: 8px 12px; text-align: left; font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; }
            .aug-tech-table thead th:first-child { border-radius: 4px 0 0 0; }
            .aug-tech-table thead th:last-child { border-radius: 0 4px 0 0; }
            .aug-tech-table tbody td { padding: 8px 12px; border-bottom: 1px solid #E8ECF5; }
            .aug-tech-table tbody tr:nth-child(even) { background: #F9FAFE; }
            .aug-tech-table tbody tr:hover { background: #EEF2FB; }
            .aug-tech-table code { background: #F0F3FA; padding: 2px 6px; border-radius: 3px; font-size: 11px; color: #0D2760; }
        </style>

        <div class="aug-tabs">
            <input type="radio" id="aug-tab1" name="aug-tabs" checked="checked" />
            <input type="radio" id="aug-tab2" name="aug-tabs" />
            <div class="aug-tab-labels">
                <label for="aug-tab1">📦 Dépendances</label>
                <label for="aug-tab2">⚙ Technique</label>
            </div>

            <!-- ONGLET 1 : DÉPENDANCES -->
            <div class="aug-tab-panel aug-panel-1">
                <div class="aug-tech-section">
                    <div class="aug-tech-title">Modules Odoo requis</div>
                    <p style="color: #333333; font-size: 12px; line-height: 1.7; margin-bottom: 12px;">
                        Ce module nécessite l'installation préalable des modules suivants :
                    </p>
                    <div>
                        <span class="aug-badge">base</span>
                    </div>
                </div>
                <div class="aug-tech-section" style="margin-bottom: 0;">
                    <div class="aug-tech-title">Modules optionnels</div>
                    <p style="color: #999; font-size: 12px; font-style: italic;">Aucun module optionnel requis.</p>
                </div>
            </div>

            <!-- ONGLET 2 : TECHNIQUE -->
            <div class="aug-tab-panel aug-panel-2">
                <div class="aug-tech-section">
                    <div class="aug-tech-title">Vues impactées</div>
                    <table class="aug-tech-table">
                        <thead><tr><th>Vue</th><th>Type</th><th>Modèle</th></tr></thead>
                        <tbody>
                            <tr><td><code>xml_id</code></td><td>Type</td><td><code>model.name</code></td></tr>
                        </tbody>
                    </table>
                </div>
                <div class="aug-tech-section">
                    <div class="aug-tech-title">Groupes de sécurité &amp; Droits</div>
                    <table class="aug-tech-table">
                        <thead><tr><th>Groupe</th><th>XML ID</th><th>Lecture</th><th>Écriture</th><th>Création</th><th>Suppression</th></tr></thead>
                        <tbody>
                            <tr>
                                <td><span class="aug-badge-outline">Utilisateur</span></td>
                                <td><code>group_xml_id</code></td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #E74C3C; font-weight: 700; text-align: center;">✗</td>
                            </tr>
                            <tr>
                                <td><span class="aug-badge">Manager</span></td>
                                <td><code>group_xml_id</code></td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                                <td style="color: #27AE60; font-weight: 700; text-align: center;">✓</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="aug-tech-section" style="margin-bottom: 0;">
                    <div class="aug-tech-title">Modèles de données</div>
                    <table class="aug-tech-table">
                        <thead><tr><th>Modèle</th><th>Description</th><th>Type</th></tr></thead>
                        <tbody>
                            <tr>
                                <td><code>model.name</code></td>
                                <td>Description</td>
                                <td><span class="aug-badge-outline">Persistant</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- PIED DE CARTOUCHE -->
        <div style="border: 2px solid #185ADB; border-radius: 4px; overflow: hidden; margin-top: 32px;">
            <div style="background: #FFBA00; height: 4px; width: 100%;"></div>
            <div style="display: flex; justify-content: space-between; align-items: center; padding: 10px 24px; background: #F5F5F5; font-size: 11px; color: #333333;">
                <div><span style="font-weight: 700; color: #0D2760;">Auguria</span> — Consultant &amp; Intégrateur Odoo — Nantes &amp; Paris</div>
                <div><a href="https://auduria.fr" style="color: #185ADB; font-weight: 600; text-decoration: none;">auduria.fr</a></div>
            </div>
            <div style="background: #FFBA00; height: 4px; width: 100%;"></div>
        </div>

    </div>
</section>
```

> **Note** : Remplacer `{LOGO_BASE64}` par la chaîne base64 complète du logo Auguria fournie dans la section 1. Remplir tous les contenus (nom, description, vues, groupes, modèles) à partir de l'analyse du code source du module.

---

## 7. Checklist de validation

Avant de livrer le module repackagé, vérifier :

- [ ] Aucune ligne vide multiple consécutive dans les XML
- [ ] Indentation uniforme 4 espaces dans tous les fichiers
- [ ] En-tête AUDURIA présent dans chaque fichier source (.py, .xml, .js, .css)
- [ ] Commentaires fonctionnels sur les classes, méthodes non triviales, et champs à logique métier
- [ ] Sections séparées par des commentaires dans les classes Python
- [ ] `__manifest__.py` complet (auteur, site web, version, catégorie, summary, description)
- [ ] `README.rst` rédigé avec le contenu fonctionnel du module
- [ ] `index.html` conforme au gabarit cartouche Auguria avec onglets remplis
- [ ] `icon.png` générée (128×128, fond bleu, pictogramme blanc, accent orange, cohérent avec le rôle)
- [ ] `web_icon` présent sur le menu root (si applicable)
- [ ] Fichiers `data` dans le manifest listés dans le bon ordre
- [ ] Pas d'import inutilisé dans les fichiers Python
- [ ] Encodage UTF-8 sur tous les fichiers

---

*Version : 2.0 — Mars 2026*
