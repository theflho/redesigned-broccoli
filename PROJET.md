# Montaigne Immobilier — Résumé du projet

Site vitrine immobilier haut de gamme sur Webflow. Les pages de détail et de listing utilisent des **embeds HTML personnalisés** pour dépasser les limites du design Webflow natif.

---

## Fichiers

| Fichier | Rôle |
|--------|------|
| `Montaigne.html` | Embed page fiche bien (détail d'un bien) |
| `autres-biens.html` | Embed page listing (grille de biens) |
| `INSTRUCTIONS-autres-biens.md` | Guide de branchement Webflow pour `autres-biens.html` |
| `PROJET.md` | Ce fichier |

---

## Montaigne.html — Fiche bien

### Sections
- **Hero** : prix, nom, surface, chambres, ville + grande image avec bouton galerie
- **Description** : texte libre CMS ("L'Esprit du Lieu")
- **Galerie** : carrousel horizontal avec lightbox (flèches desktop, swipe mobile)
- **Détails** : tableau de specs conditionnel (masque les champs vides)
- **DPE / GES** : barres de notation énergétique avec barre active mise en valeur
- **Contact** : Ophélie + Christophe + email + lien Géorisques

### Champs CMS utilisés
| Champ Webflow | Contenu |
|---------------|---------|
| `price` | Prix de vente (formaté automatiquement en `385 000 €`) |
| `name` | Nom du bien |
| `image2` | Image principale (hero) |
| `description` | Texte de description |
| `area` | Surface en m² |
| `bed` | Nombre de chambres |
| `bathroom` | Salles de bain |
| `parking-box` | Parking / box |
| `terrain` | Surface terrain m² |
| `taxe-fonciere` | Taxe foncière €/an |
| `renovate` | Type de bien |
| `los-angeles` | Ville |
| `note-dpe-3` | Lettre DPE (A à G) |
| `classe-energie` | Consommation kWh/m²/an |
| `notes-ges` | Lettre GES (A à G) |
| `consommation-ges` | Émissions kgCO₂/m²/an |

### Fonctionnalités JS
- Prix formaté en fr-FR + calcul automatique du prix au m²
- Specs conditionnelles (lignes masquées si champ CMS vide)
- DPE/GES : barre active détectée et mise en valeur
- Carrousel : drag souris + swipe mobile natif
- Lightbox : crossfade 2 images (portrait ↔ paysage sans overlap), flèches desktop, swipe mobile
- Scroll lock iOS quand lightbox ouverte (`position: fixed` sur body)
- Bouton Partager : Web Share API ou copie du lien

---

## autres-biens.html — Listing

### Fonctionnalités
- Grille responsive : 3 col. desktop / 2 tablette / 1 mobile
- Carte : image + prix + nom + specs + ville
- Hover : élévation + zoom image
- Prix formaté automatiquement

---

## Palette "Lin doré adouci"

| Rôle | Couleur |
|------|---------|
| Fond principal | `#f8f5ef` |
| Accent / bordures | `#c8b3a0` |
| Texte secondaire | `#635749` |
| Bordures légères | `#e6deda` |
| Hover fond | `#eee9e3` |
| Texte principal | `#1a1a1a` |

---

## Couleurs DPE officielles (ADEME)

`A #00a06d` `B #52b153` `C #a5cb74` `D #f4e70f` `E #f0b50f` `F #eb8235` `G #d7221f`

## Couleurs GES officielles

`A #a4dbf8` `B #8cb4d3` `C #7792b1` `D #606f8f` `E #4d5271` `F #393551` `G #281b35`

---

## Points d'attention

- Le champ "ville" utilise le slug Webflow `los-angeles` (nom de champ hérité, ne pas renommer)
- `initSpecs` utilise un retry loop : les champs CMS peuvent arriver après le premier rendu
- La lightbox crée un `#lb-overlay` en bas du `<body>` au chargement — normal
- Sur iOS, le scroll lock utilise `position: fixed` sur le body (l'`overflow: hidden` seul ne suffit pas)
