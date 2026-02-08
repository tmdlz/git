# TP04 - Branching et Workflow de Développement

## 🎯 Objectifs

- Créer et gérer des branches
- Basculer entre les branches
- Comprendre le workflow Git Flow
- Développer des features en parallèle

## 📝 Contexte

Vous travaillez sur une application e-commerce. Vous devez développer deux nouvelles fonctionnalités en parallèle : un système de panier et un système de wishlist, tout en maintenant une branche principale stable.

## 🔧 Instructions

### Étape 1 : Initialisation

1. Créez `ecommerce-app` et initialisez Git
2. Créez `index.html` avec :
```html
<!DOCTYPE html>
<html>
<head><title>E-Commerce</title></head>
<body>
    <h1>Bienvenue dans notre boutique</h1>
</body>
</html>
```
3. Commitez "Initial e-commerce structure"

### Étape 2 : Feature Branch - Panier

4. Créez une branche `feature/cart`
5. Basculez sur cette branche
6. Ajoutez dans `index.html` :
```html
<div id="cart">
    <h2>Panier</h2>
    <ul id="cart-items"></ul>
</div>
```
7. Créez `cart.js` :
```javascript
const cart = [];
function addToCart(item) {
    cart.push(item);
}
```
8. Commitez "Add shopping cart feature"
9. Modifiez `cart.js` pour ajouter :
```javascript
function removeFromCart(index) {
    cart.splice(index, 1);
}
```
10. Commitez "Add remove from cart functionality"

### Étape 3 : Feature Branch - Wishlist

11. Retournez sur `main`
12. Créez et basculez sur `feature/wishlist`
13. Ajoutez dans `index.html` :
```html
<div id="wishlist">
    <h2>Liste de souhaits</h2>
    <ul id="wishlist-items"></ul>
</div>
```
14. Créez `wishlist.js` :
```javascript
const wishlist = [];
function addToWishlist(item) {
    wishlist.push(item);
}
```
15. Commitez "Add wishlist feature"

### Étape 4 : Development Branch

16. Retournez sur `main`
17. Créez une branche `develop`
18. Listez toutes vos branches
19. Affichez la branche courante

### Étape 5 : Visualisation

20. Affichez le graphe de toutes les branches
21. Affichez l'historique de `feature/cart`
22. Comparez `main` et `feature/cart`

## ✅ Validation

```bash
# Nombre de branches
git branch

# Commits sur feature/cart
git log feature/cart --oneline

# Différences entre main et feature/wishlist
git diff main feature/wishlist
```

---

# TP05 - Merge et Résolution de Conflits

## 🎯 Objectifs

- Merger des branches
- Créer et résoudre des conflits
- Comprendre fast-forward vs merge commit
- Gérer des merges complexes

## 📝 Contexte

Suite au TP04, vous devez maintenant intégrer vos features dans la branche principale, mais vous allez rencontrer des conflits à résoudre.

## 🔧 Instructions

### Étape 1 : Merge simple (fast-forward)

1. Assurez-vous d'être sur `main`
2. Mergez `feature/cart` dans `main`
3. Observez le type de merge (fast-forward ou merge commit ?)
4. Vérifiez que les fichiers de cart sont dans main

### Étape 2 : Préparer un conflit

5. Sur `main`, modifiez `index.html` :
```html
<body>
    <h1>Bienvenue dans notre super boutique</h1>
    <p>Les meilleurs produits au meilleur prix</p>
</body>
```
6. Commitez "Update homepage message on main"

7. Basculez sur `feature/wishlist`
8. Modifiez `index.html` :
```html
<body>
    <h1>Bienvenue dans notre boutique en ligne</h1>
    <p>Découvrez nos nouveautés</p>
</body>
```
9. Commitez "Update homepage message on wishlist"

### Étape 3 : Créer le conflit

10. Retournez sur `main`
11. Tentez de merger `feature/wishlist`
12. Git devrait signaler un conflit

### Étape 4 : Résoudre le conflit

13. Ouvrez `index.html` et examinez les marqueurs de conflit
14. Décidez de la résolution (gardez les deux messages ou choisissez-en un)
15. Résolvez en gardant :
```html
<body>
    <h1>Bienvenue dans notre super boutique en ligne</h1>
    <p>Découvrez nos meilleurs produits et nouveautés</p>
</body>
```
16. Ajoutez le fichier résolu
17. Finalisez le merge avec un commit

### Étape 5 : Conflit multi-fichiers

18. Créez une branche `feature/footer`
19. Ajoutez dans `index.html` un footer :
```html
<footer>Copyright 2024</footer>
```
20. Créez `footer.css` :
```css
footer { background: #333; color: white; }
```
21. Commitez "Add footer"

22. Retournez sur `main`
23. Ajoutez un footer différent :
```html
<footer>© 2024 - Tous droits réservés</footer>
```
24. Commitez "Add copyright footer"

25. Mergez `feature/footer` et résolvez les conflits

### Étape 6 : Merge avec --no-ff

26. Créez une branche `feature/search`
27. Ajoutez une barre de recherche
28. Commitez
29. Retournez sur main
30. Mergez avec `--no-ff` pour forcer un merge commit

## ✅ Validation

```bash
# Voir l'historique avec les merges
git log --graph --oneline --all

# Vérifier qu'il n'y a plus de conflits
git status

# Nombre de merge commits
git log --merges --oneline
```

---

# TP06 - Collaboration avec GitHub

## 🎯 Objectifs

- Créer un dépôt distant sur GitHub
- Pousser du code vers GitHub
- Cloner un dépôt
- Synchroniser local et remote

## 📝 Contexte

Votre projet local doit maintenant être partagé avec votre équipe via GitHub. Vous allez apprendre à synchroniser votre travail.

## 🔧 Instructions

### Étape 1 : Créer le dépôt GitHub

1. Connectez-vous à GitHub
2. Créez un nouveau repository `ecommerce-app`
3. Ne cochez PAS "Initialize with README"
4. Créez le repository

### Étape 2 : Connecter local et remote

5. Copiez l'URL HTTPS du repository
6. Ajoutez le remote :
```bash
git remote add origin <URL>
```
7. Vérifiez les remotes configurés
8. Poussez `main` vers GitHub
9. Vérifiez sur GitHub que les fichiers sont là

### Étape 3 : Pousser les branches

10. Poussez `feature/cart` vers GitHub
11. Poussez `feature/wishlist` vers GitHub
12. Sur GitHub, vérifiez que vous voyez toutes les branches

### Étape 4 : Modifications distantes

13. Sur GitHub, éditez `README.md` directement
14. Ajoutez du contenu et commitez sur GitHub
15. En local, récupérez les changements avec `fetch`
16. Comparez local et remote
17. Mergez avec `pull`

### Étape 5 : Workflow collaboratif

18. Créez une nouvelle branche `feature/payment`
19. Ajoutez du code pour un système de paiement
20. Commitez
21. Poussez cette branche sur GitHub
22. Sur GitHub, modifiez le même fichier
23. En local, modifiez aussi
24. Poussez - que se passe-t-il ?
25. Résolvez avec pull puis push

### Étape 6 : Cloner dans un autre dossier

26. Sortez du projet
27. Clonez votre repository dans un nouveau dossier
28. Vérifiez les branches disponibles
29. Créez une branche locale depuis une remote
30. Faites des modifications et poussez

## ✅ Validation

```bash
# Voir tous les remotes
git remote -v

# Voir toutes les branches (local + remote)
git branch -a

# État de synchronisation
git status

# Historique des pushs
git log --oneline origin/main
```

## 🎓 Questions

1. Différence entre `fetch` et `pull` ?
2. Pourquoi utiliser `git push -u origin main` ?
3. Comment supprimer une branche sur GitHub ?
4. Que faire si le push est rejeté ?

---

⚠️ **Réponses dans les fichiers correspondants**
