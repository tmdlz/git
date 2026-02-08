# TP01 - Initialisation et Premiers Commits

## 🎯 Objectifs

- Initialiser un dépôt Git local
- Créer et modifier des fichiers
- Comprendre le concept de commit
- Utiliser `git status`, `git add`, et `git commit`

## 📝 Contexte

Vous démarrez un nouveau projet web pour un site de portfolio. Vous devez mettre en place le système de versioning dès le début du projet.

## 🔧 Instructions

### Étape 1 : Préparation du projet

1. Créez un dossier nommé `portfolio-website`
2. Naviguez dans ce dossier
3. Créez les fichiers suivants :
   - `index.html`
   - `style.css`
   - `README.md`

### Étape 2 : Initialisation Git

4. Initialisez un dépôt Git dans ce dossier
5. Vérifiez que le dossier `.git` a bien été créé

### Étape 3 : Premier contenu

6. Ajoutez le contenu suivant dans `index.html` :
```html
<!DOCTYPE html>
<html>
<head>
    <title>Mon Portfolio</title>
</head>
<body>
    <h1>Bienvenue sur mon portfolio</h1>
</body>
</html>
```

7. Ajoutez le contenu suivant dans `style.css` :
```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
}
```

8. Ajoutez le contenu suivant dans `README.md` :
```markdown
# Portfolio Website

Site de portfolio personnel en cours de développement.
```

### Étape 4 : Premier commit

9. Vérifiez l'état de votre dépôt
10. Ajoutez tous les fichiers à la staging area
11. Créez un commit avec le message "Initial commit: add basic structure"
12. Vérifiez l'historique des commits

### Étape 5 : Modification et second commit

13. Modifiez `index.html` pour ajouter un paragraphe :
```html
<p>Développeur passionné par les nouvelles technologies.</p>
```

14. Modifiez `style.css` pour ajouter :
```css
h1 {
    color: #333;
    text-align: center;
}
```

15. Vérifiez l'état de votre dépôt
16. Ajoutez uniquement le fichier `index.html` à la staging area
17. Créez un commit avec le message "Add welcome paragraph"
18. Ajoutez maintenant `style.css` et commitez avec le message "Add h1 styling"

## ✅ Validation

Vérifiez que :

```bash
# Vous devez voir 3 commits
git log --oneline

# Le dépôt doit être propre
git status

# Vous devez voir le dossier .git
ls -la
```

## 🎓 Questions de réflexion

1. Pourquoi avons-nous fait deux commits séparés pour `index.html` et `style.css` ?
2. Que signifie "working directory clean" ?
3. Que contient le dossier `.git` ?

## 📚 Commandes utilisées

À remplir par vous-même après avoir complété le TP :

- Initialiser un dépôt : `_______________`
- Voir l'état : `_______________`
- Ajouter des fichiers : `_______________`
- Commiter : `_______________`
- Voir l'historique : `_______________`

---

⚠️ **Ne consultez les réponses qu'après avoir essayé !**

Réponses disponibles dans : `TP01-REPONSES.md`
