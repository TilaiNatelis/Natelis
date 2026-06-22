# Thème Shopify — Natélis en Provence

Thème Liquid recréant la maquette Claude Design « Natélis - Site ». Toutes les données
dynamiques (produits, collections, blog, panier) sont branchées sur les objets Shopify.

## Structure

```
theme/
├── layout/theme.liquid          Gabarit global (charge le CSS, l'en-tête, le pied, la newsletter)
├── assets/natelis.css           Charte graphique (couleurs, polices, composants)
├── snippets/
│   ├── main-nav.liquid          Menu principal (menu Shopify "main-menu")
│   └── product-card.liquid      Carte produit réutilisable
├── sections/
│   ├── announcement-bar.liquid  Bandeau promo
│   ├── header.liquid            En-tête (logo, recherche, compte, panier)
│   ├── footer.liquid            Pied de page
│   ├── newsletter.liquid        Bloc newsletter
│   ├── home-*.liquid            Sections de la page d'accueil
│   ├── main-product.liquid      Fiche produit
│   ├── main-collection.liquid   Page collection (filtres par objectif)
│   ├── main-cart.liquid         Panier
│   ├── main-blog.liquid         Blog
│   ├── main-article.liquid      Article
│   ├── page-conseils.liquid     Page Conseils (étapes, FAQ, univers)
│   ├── page-automne.liquid      Page Sélection d'automne
│   └── page-diagnostic.liquid   Diagnostic interactif (quiz + reco)
├── templates/                   Gabarits JSON associant chaque page à sa section
└── config/                      settings_schema.json / settings_data.json
```

## Installation

**Option A — Shopify CLI (recommandé)**
```bash
cd theme
shopify theme dev      # prévisualisation locale
shopify theme push     # envoi vers la boutique
```

**Option B — Admin Shopify**
Zipper le dossier `theme/` puis : *Boutique en ligne › Thèmes › Ajouter › Importer un thème*.

## Configuration après installation

1. **Produits** : créer les 13 produits (voir `../natelis-shopify-content.md`).
   - **Tags** = objectifs (Immunité, Sommeil, Stress, Beauté, Articulations, Énergie, Digestion)
   - **Tags** `Best-seller` / `Nouveau` pour afficher les badges.
   - Métachamps (facultatifs) à créer dans *Paramètres › Métachamps › Produits* :
     - `custom.subtitle` (texte) — sous-titre de la carte
     - `custom.rating` (décimal) — note (ex. 4.8)
     - `custom.rating_count` (entier) — nombre d'avis
     - `custom.benefits` (liste de textes) — bénéfices affichés sur la fiche
   - Variantes « Format » : Cure 1 mois / Cure 3 mois ×3.

2. **Collections** (automatiques par tag) : Tous les compléments, Immunité, Sommeil, Stress,
   Beauté, Articulations, Énergie, Digestion, Meilleures ventes, Nouveautés, Sélection d'automne,
   Vitalité & immunité, Beauté & sommeil, Sport & bien-être.

3. **Menus** (*Navigation*) :
   - `main-menu` : Sélection d'automne · Nouveautés · Produits · Conseils · Blog · Diagnostic
   - 3 menus pour les colonnes du pied de page (Produits / La marque / Aide).

4. **Pages** : créer 3 pages et leur affecter le bon gabarit (champ « Modèle de thème ») :
   - Page « Sélection d'automne » → modèle `automne`
   - Page « Conseils » → modèle `conseils`
   - Page « Diagnostic » → modèle `diagnostic`

5. **Blog** : créer le blog « Carnet de la vigne » et les 6 articles (contenu dans le `.md`).

6. **Personnalisation** : *Personnaliser le thème* pour choisir le logo, les images du hero,
   les images des cartes univers et les collections affichées.

## Notes

- Le **diagnostic** est 100 % fonctionnel côté client : il lit les produits de la collection
  choisie, applique le scoring (Q1 ×2, Q2/Q3 ×1), garde les 2 objectifs majeurs et recommande
  jusqu'à 4 produits, avec ajout de la routine au panier via `/cart/add.js`.
- Les **notes/avis** affichés viennent des métachamps (valeurs indicatives). Pour de vrais
  avis, brancher une app (Judge.me, Loox).
- La charte (couleurs, polices) est centralisée dans `assets/natelis.css` via des variables CSS.
