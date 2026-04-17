# Instructions — Embed `autres-biens.html`

Fichier embed Webflow pour afficher la grille de biens de l'agence depuis le CMS.

---

## 1. Créer la page dans Webflow

1. Crée une nouvelle page (ex: `/nos-biens`)
2. Ajoute un **Embed** en haut de page et colle le contenu de `autres-biens.html` dedans

---

## 2. Ajouter la Collection List

1. Dans Webflow, insère un **Collection List** lié à ta collection de biens
2. Place ce Collection List **à l'intérieur de l'Embed** — ou juste en dessous si Webflow ne le permet pas (l'embed stylise les éléments présents dans la page)

> ⚠️ Important : le Collection List doit se trouver **dans** le div `.autresbiens-wrap` pour que les styles s'appliquent. Si ce n'est pas possible, place l'embed et le Collection List au même niveau et ajuste le CSS en retirant `.autresbiens-wrap` des sélecteurs.

---

## 3. Structurer chaque item du Collection List

Dans le **template** de la Collection List (l'item), construire la structure suivante :

```
.w-dyn-item
└── Link Block  →  classe : carte-bien  →  lié au slug du bien
    ├── Div  →  classe : img-bien-wrap
    │   └── Image  →  classe : img-bien  →  liée au champ image2
    └── Div  →  classe : carte-bien-infos
        ├── Text  →  classe : prix-bien   →  lié au champ price
        ├── Text  →  classe : nom-bien    →  lié au champ name
        ├── Div   →  classe : separateur-bien  (vide)
        ├── Div   →  classe : specs-bien
        │   ├── Text  →  lié à area + " m²"
        │   └── Text  →  lié à bed + " ch."
        └── Text  →  classe : ville-bien  →  lié au champ los-angeles
```

---

## 4. Champs CMS utilisés

| Classe Webflow | Champ CMS      | Exemple de valeur |
|----------------|----------------|-------------------|
| `prix-bien`    | `price`        | `385000`          |
| `nom-bien`     | `name`         | `Maison avec garage` |
| `img-bien`     | `image2`       | (image de couverture) |
| `specs-bien`   | `area` + `bed` | `120 m² — 4 ch.`  |
| `ville-bien`   | `los-angeles`  | `Bois-Guillaume`  |

---

## 5. Comportement automatique

- **Prix** : formaté automatiquement en `385 000 €` (séparateur de milliers français)
- **Grille responsive** : 3 colonnes desktop / 2 tablette / 1 mobile
- **Hover** : élévation de la carte + léger zoom sur l'image

---

## 6. Personnalisation rapide

| Ce que tu veux changer | Où dans le CSS          | Valeur actuelle |
|------------------------|-------------------------|-----------------|
| Hauteur des images     | `.img-bien`             | `260px`         |
| Espacement entre cartes| `.w-dyn-items`          | `gap: 32px`     |
| Colonnes desktop       | `.w-dyn-items`          | `repeat(3, 1fr)`|
| Colonnes tablette      | `@media max-width 1100px` | `repeat(2, 1fr)` |
