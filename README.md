# Jeu de cartes — Contrat Transilien × Île-de-France Mobilités

Application web **statique** et **autonome** pour digitaliser le jeu de cartes pédagogique
consacré au contrat Transilien × Île-de-France Mobilités.

- Un seul fichier : [`index.html`](index.html) (HTML + CSS + JavaScript).
- Aucune dépendance, aucun framework, aucun CDN — fonctionne **hors ligne**.
- Toutes les cartes sont des images PNG du dossier [`images/`](images/).

## Lancer l'application en local

- **Le plus simple :** double-cliquez sur `index.html` (il s'ouvre dans le navigateur).
- **Via un serveur local** (recommandé sur tablette / pour tester GitHub Pages) :
  ```bash
  cd <dossier-du-projet>
  python3 -m http.server 8000
  # puis ouvrez http://localhost:8000
  ```

## Comment jouer

1. **Accueil** : présentation + bouton « Commencer ».
2. **Étape 1** : découvrir les 6 indicateurs (cliquez une carte pour l'agrandir).
3. **Étape 2** : placer les 14 sous-indicateurs **au-dessus** du bon indicateur.
4. **Étape 3** : placer les 27 métiers **sous** le bon indicateur.
5. **Fin** : score, réussites du premier coup, erreurs et badge.

Glisser-déposer **à la souris, au trackpad et au tactile** (Pointer Events).
Mode de secours : **cliquez la carte** active puis **cliquez la zone** cible.

## Personnaliser le jeu

Tout est regroupé en haut du `<script>` dans `index.html` :

| Pour modifier… | Éditez la constante… |
|---|---|
| Les images des cartes | remplacez les fichiers dans `images/` (mêmes noms) |
| Les indicateurs et leurs titres | `INDICATEURS` |
| La correspondance sous-indicateur → indicateur | `SOUS_INDICATEURS` (champ `cible`) |
| La correspondance métier → indicateur | `METIERS` (champ `cible`) |
| Le dos de carte | `DOS_CARTE` |
| Les seuils et textes de badge | `SEUILS_BADGE` (champ `maxErreurs`) |

**Remplacer une image :** déposez un PNG portrait dans `images/` en conservant exactement
le nom attendu (`indicateur1.png`, `sousindicateur1.png`, `metier1.png`, `doscarte.png`, …).
Si un fichier manque, l'application affiche un message d'erreur indiquant le nom manquant.

## Publier sur GitHub Pages

```bash
# 1) Créer le dépôt sur github.com (ex. : jeu-contrat-transilien), puis :
git remote add origin https://github.com/<votre-compte>/<votre-depot>.git
git push -u origin main

# 2) Activer GitHub Pages :
#    Settings → Pages → Source : "Deploy from a branch"
#    Branch : main / (root) → Save
# 3) L'URL publique apparaît dans Settings → Pages au bout de ~1 minute :
#    https://<votre-compte>.github.io/<votre-depot>/
```

Avec GitHub CLI (`gh`) authentifié, tout se fait en une commande :

```bash
gh repo create <votre-depot> --public --source=. --remote=origin --push
gh api -X POST repos/<votre-compte>/<votre-depot>/pages \
  -f source.branch=main -f source.path=/
```

Aucun build n'est nécessaire : le projet est directement publiable.
