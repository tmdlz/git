# TP02 - RÉPONSES

## 📋 Solution complète

### Étape 1 : Préparation du projet

```bash
# Créer le dossier
mkdir webapp-project
cd webapp-project

# Initialiser Git
git init

# Créer la structure
mkdir -p src/components
mkdir styles

# Créer les fichiers
touch index.html config.json
touch src/app.js src/utils.js src/components/navbar.js
touch styles/main.css styles/responsive.css
```

### Étape 2 : Contenu des fichiers

```bash
# Vous pouvez utiliser echo ou votre éditeur
echo '<!DOCTYPE html>
<html>
<head><title>Web App</title></head>
<body><h1>My Web App</h1></body>
</html>' > index.html

echo 'console.log("App started");' > src/app.js
echo 'function helper() { return true; }' > src/utils.js
echo 'const navbar = { brand: "MyApp" };' > src/components/navbar.js
echo 'body { margin: 0; }' > styles/main.css
echo '@media (max-width: 768px) { body { padding: 10px; } }' > styles/responsive.css
echo '{ "version": "1.0.0" }' > config.json
```

### Étape 3 : Staging sélectif

```bash
# Ajouter uniquement le dossier src/
git add src/

# Vérifier
git status
```

**Résultat** :
```
Changes to be committed:
        new file:   src/app.js
        new file:   src/components/navbar.js
        new file:   src/utils.js

Untracked files:
        config.json
        index.html
        styles/
```

```bash
# Commiter
git commit -m "Add source files"
```

### Étape 4 : Staging par extension

```bash
# Ajouter uniquement les fichiers .css
git add *.css
# Cette commande depuis la racine ne fonctionnera pas car les .css sont dans un sous-dossier

# Solution correcte :
git add styles/*.css
# ou
git add styles/

# Vérifier
git status

# Commiter
git commit -m "Add stylesheets"
```

**Point important** : `git add *.css` depuis la racine ne trouve pas les fichiers dans les sous-dossiers. Il faut spécifier le chemin ou utiliser `git add **/*.css` (sur certains systèmes).

### Étape 5 : Staging global

```bash
# Ajouter tout ce qui reste
git add .
# ou
git add -A
# ou
git add --all

# Vérifier
git status

# Commiter
git commit -m "Add remaining files"
```

### Étape 6 : Modifications multiples

```bash
# Modifier index.html
echo '<p>Version 1.0</p>' >> index.html

# Modifier app.js
echo 'console.log("Version 1.0");' >> src/app.js

# Supprimer config.json (manuellement ou avec rm)
rm config.json

# Créer README.md
echo '# Web App Project

Application web en développement.' > README.md

# Vérifier
git status
```

**Résultat** :
```
Changes not staged for commit:
        modified:   index.html
        modified:   src/app.js
        deleted:    config.json

Untracked files:
        README.md
```

### Étape 7 : Staging différencié

```bash
# Vérifier l'état
git status

# Ajouter seulement index.html et README.md
git add index.html README.md

# Vérifier
git status
```

**Résultat** :
```
Changes to be committed:
        modified:   index.html
        new file:   README.md

Changes not staged for commit:
        modified:   src/app.js
        deleted:    config.json
```

```bash
# Commiter
git commit -m "Update index and add README"
```

### Étape 8 : Unstaging

```bash
# Ajouter app.js
git add src/app.js

# Vérifier qu'il est staged
git status

# Unstage le fichier
git restore --staged src/app.js
# ou (ancienne méthode)
git reset HEAD src/app.js

# Vérifier
git status
```

**Résultat** : `src/app.js` est de retour dans "Changes not staged for commit"

**Note** : Les modifications ne sont PAS perdues, le fichier est juste retiré de la staging area.

### Étape 9 : Gestion des suppressions

```bash
# Supprimer avec Git (supprime ET stage)
git rm src/utils.js

# Vérifier
git status
```

**Résultat** :
```
Changes to be committed:
        deleted:    src/utils.js

Changes not staged for commit:
        modified:   src/app.js
        deleted:    config.json
```

```bash
# Commiter
git commit -m "Remove unused utils file"
```

**Différence importante** :
- `rm fichier` puis `git add fichier` = 2 étapes
- `git rm fichier` = 1 étape (supprime ET stage)

### Étape 10 : Staging avec `git add *`

```bash
# Créer les fichiers tests
touch test1.txt test2.txt

# Vérifier l'état
git status

# Naviguer dans src/
cd src/

# Ajouter avec *
git add *

# Vérifier depuis src/
git status
```

**Résultat** : Seul `app.js` (qui est modifié dans ce dossier) est staged.

```bash
# Retourner à la racine
cd ..

# Utiliser git add .
git add .

# Vérifier
git status
```

**Résultat** : Maintenant TOUT est staged (test1.txt, test2.txt, src/app.js, et la suppression de config.json).

**Différence clé** :
- `git add *` : N'ajoute QUE les fichiers visibles dans le dossier courant (pas les fichiers supprimés)
- `git add .` : Ajoute TOUT depuis le dossier courant, y compris les suppressions

```bash
# Commiter
git commit -m "Add test files and update app.js"
```

## ✅ Validation finale

```bash
# Vérifier les commits
git log --oneline
```

**Résultat attendu** : Au moins 5 commits
```
abc1234 Add test files and update app.js
def5678 Remove unused utils file
ghi9012 Update index and add README
jkl3456 Add remaining files
mno7890 Add stylesheets
pqr1234 Add source files
```

```bash
# Voir les fichiers supprimés dans l'historique
git log --diff-filter=D --summary
```

```bash
# État final
git status
```

**Résultat** : `nothing to commit, working tree clean`

## 🎓 Réponses aux questions de réflexion

### 1. Différence entre `git add .`, `git add -A`, et `git add *`

| Commande | Comportement | Suppressions | Scope |
|----------|--------------|--------------|-------|
| `git add .` | Ajoute tout depuis le dossier courant | ✅ Oui | Récursif |
| `git add -A` | Ajoute tout dans le dépôt entier | ✅ Oui | Tout le dépôt |
| `git add *` | Ajoute les fichiers visibles (expansion shell) | ❌ Non | Dossier courant |

**Exemples** :
- `git add .` depuis `src/` → ajoute tout dans src/ et sous-dossiers
- `git add -A` depuis n'importe où → ajoute TOUT dans le dépôt
- `git add *` → expansion par le shell, ignore les fichiers cachés et suppressions

### 2. Pourquoi `git add *` n'ajoute pas les fichiers supprimés ?

Le `*` est une **expansion du shell**, pas une commande Git.

Quand vous tapez `git add *`, votre shell (bash, zsh, etc.) transforme d'abord `*` en liste de fichiers **visibles**.

```bash
# Ce que vous tapez :
git add *

# Ce que le shell exécute :
git add file1.js file2.css folder1 folder2
```

Les fichiers **supprimés** n'existent plus dans le système de fichiers, donc ils ne sont pas dans l'expansion. Git ne les "voit" jamais dans cette commande.

`git add .` est une **vraie commande Git** qui inspecte le dépôt Git, pas juste le système de fichiers.

### 3. Comment unstager un fichier sans perdre les modifications ?

**Méthode moderne (Git 2.23+)** :
```bash
git restore --staged <fichier>
```

**Ancienne méthode (toujours valide)** :
```bash
git reset HEAD <fichier>
```

Les deux ramènent le fichier de "Changes to be committed" vers "Changes not staged", **sans toucher aux modifications**.

Pour **tout** unstager :
```bash
git restore --staged .
# ou
git reset HEAD
```

### 4. Différence entre `git rm` et suppression manuelle ?

| Action | Suppression système | Staging |
|--------|-------------------|---------|
| `rm fichier` puis `git add fichier` | ✅ | ✅ (2 étapes) |
| `git rm fichier` | ✅ | ✅ (1 étape) |

`git rm` = `rm` + `git add` en une seule commande.

**Cas particuliers** :

```bash
# Supprimer du Git mais garder en local
git rm --cached fichier

# Forcer la suppression d'un fichier modifié
git rm -f fichier

# Supprimer un dossier récursivement
git rm -r dossier/
```

## 📚 Tableau récapitulatif des commandes

| Commande | Action |
|----------|--------|
| `git add <fichier>` | Stage un fichier spécifique |
| `git add .` | Stage tout depuis le dossier courant (+ suppressions) |
| `git add -A` | Stage tout dans le dépôt (+ suppressions) |
| `git add *` | Stage les fichiers visibles (PAS les suppressions) |
| `git add *.ext` | Stage tous les fichiers avec extension .ext |
| `git add dossier/` | Stage tout un dossier |
| `git restore --staged <fichier>` | Unstage un fichier |
| `git reset HEAD <fichier>` | Unstage un fichier (ancienne méthode) |
| `git rm <fichier>` | Supprime ET stage |
| `git rm --cached <fichier>` | Retire de Git, garde en local |
| `git rm -r dossier/` | Supprime un dossier récursivement |

## 💡 Points clés à retenir

1. **Utilisez `git add .` par défaut** : C'est le plus fiable et prévisible
2. **`git add *` peut surprendre** : N'oublie les fichiers supprimés
3. **`git add -A`** : Équivalent à `git add .` depuis la racine
4. **Unstaging ≠ Annulation** : Unstager ne perd pas les modifications
5. **`git rm`** : Raccourci pour supprimer + stage

## 🚀 Astuces avancées

### Voir ce qui est dans la staging area

```bash
# Différences entre staging et dernier commit
git diff --staged
# ou
git diff --cached
```

### Ajouter interactivement

```bash
# Mode interactif pour choisir précisément
git add -p
# Git vous demandera pour chaque modification
```

### Patterns avancés

```bash
# Tous les .js sauf dans node_modules
git add '*.js' ':!node_modules'

# Tous les fichiers dans src/ et subdirectories
git add 'src/**/*'
```

---

**Excellent travail ! Vous maîtrisez maintenant le staging ! 🎉**

Passez au TP03 pour explorer la navigation dans l'historique.
