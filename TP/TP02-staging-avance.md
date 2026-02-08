# TP02 - Gestion Avancée du Staging

## 🎯 Objectifs

- Maîtriser les différentes variantes de `git add`
- Comprendre la différence entre `git add .`, `git add -A`, et `git add *`
- Savoir unstage des fichiers
- Gérer les suppressions de fichiers avec Git

## 📝 Contexte

Vous travaillez sur une application web avec plusieurs composants. Vous devez apprendre à gérer finement quels fichiers sont ajoutés à la staging area, surtout dans une structure de dossiers complexe.

## 🔧 Instructions

### Étape 1 : Préparation du projet

1. Créez un nouveau dossier `webapp-project`
2. Initialisez Git dans ce dossier
3. Créez la structure suivante :

```
webapp-project/
├── src/
│   ├── app.js
│   ├── utils.js
│   └── components/
│       └── navbar.js
├── styles/
│   ├── main.css
│   └── responsive.css
├── index.html
└── config.json
```

### Étape 2 : Contenu des fichiers

4. Ajoutez du contenu dans chaque fichier :

**index.html** :
```html
<!DOCTYPE html>
<html>
<head><title>Web App</title></head>
<body><h1>My Web App</h1></body>
</html>
```

**src/app.js** :
```javascript
console.log("App started");
```

**src/utils.js** :
```javascript
function helper() { return true; }
```

**src/components/navbar.js** :
```javascript
const navbar = { brand: "MyApp" };
```

**styles/main.css** :
```css
body { margin: 0; }
```

**styles/responsive.css** :
```css
@media (max-width: 768px) { body { padding: 10px; } }
```

**config.json** :
```json
{ "version": "1.0.0" }
```

### Étape 3 : Staging sélectif

5. Ajoutez UNIQUEMENT les fichiers du dossier `src/` à la staging area
6. Vérifiez avec `git status` que seuls ces fichiers sont staged
7. Faites un commit avec le message "Add source files"

### Étape 4 : Staging par extension

8. Ajoutez UNIQUEMENT les fichiers `.css` à la staging area
9. Vérifiez et commitez avec "Add stylesheets"

### Étape 5 : Staging global

10. Ajoutez tous les fichiers restants à la staging area
11. Vérifiez et commitez avec "Add remaining files"

### Étape 6 : Modifications multiples

12. Modifiez `index.html` : ajoutez `<p>Version 1.0</p>`
13. Modifiez `src/app.js` : ajoutez `console.log("Version 1.0");`
14. Supprimez le fichier `config.json` (manuellement, via votre explorateur)
15. Créez un nouveau fichier `README.md` avec du contenu

### Étape 7 : Staging différencié

16. Vérifiez l'état du dépôt
17. Ajoutez UNIQUEMENT `index.html` et `README.md` à la staging area
18. Vérifiez que `src/app.js` et la suppression de `config.json` NE sont PAS staged
19. Commitez avec "Update index and add README"

### Étape 8 : Unstaging

20. Ajoutez `src/app.js` à la staging area
21. Utilisez une commande pour unstage ce fichier
22. Vérifiez qu'il est retourné dans "Changes not staged"

### Étape 9 : Gestion des suppressions

23. Utilisez la commande Git appropriée pour supprimer `src/utils.js` ET le stager en une seule opération
24. Vérifiez avec `git status`
25. Commitez avec "Remove unused utils file"

### Étape 10 : Staging avec `git add *`

26. Créez deux nouveaux fichiers : `test1.txt` et `test2.txt`
27. Naviguez dans le dossier `src/`
28. Depuis ce dossier, utilisez `git add *`
29. Vérifiez ce qui a été staged
30. Retournez à la racine et utilisez `git add .`
31. Vérifiez la différence

## ✅ Validation

```bash
# Vous devez avoir au moins 5 commits
git log --oneline

# Vérifiez les fichiers supprimés
git log --diff-filter=D --summary

# Vérifiez l'état final
git status
```

## 🎓 Questions de réflexion

1. Quelle est la différence entre `git add .`, `git add -A`, et `git add *` ?
2. Pourquoi `git add *` n'ajoute-t-il pas les fichiers supprimés ?
3. Comment unstager un fichier sans perdre les modifications ?
4. Quelle est la différence entre `git rm` et supprimer manuellement puis `git add` ?

## 🧪 Expérimentations

Essayez ces scénarios :

- Que se passe-t-il si vous faites `git add *.js` depuis la racine ?
- Comment ajouter tous les fichiers SAUF un type spécifique ?
- Comment voir ce qui est dans la staging area ?

---

⚠️ **Ne consultez les réponses qu'après avoir essayé !**

Réponses disponibles dans : `TP02-REPONSES.md`
