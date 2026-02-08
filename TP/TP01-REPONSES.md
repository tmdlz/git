# TP01 - RÉPONSES

## 📋 Solution complète

### Étape 1 : Préparation du projet

```bash
# Créer le dossier du projet
mkdir portfolio-website

# Naviguer dans le dossier
cd portfolio-website

# Créer les fichiers
touch index.html style.css README.md
```

### Étape 2 : Initialisation Git

```bash
# Initialiser Git
git init

# Vérifier la création du dossier .git
ls -la
# ou sur Windows
dir /a
```

**Résultat attendu** : Vous devriez voir `Initialized empty Git repository in ...`

### Étape 3 : Premier contenu

```bash
# Ouvrir et éditer index.html (avec votre éditeur préféré)
# Exemple avec nano
nano index.html
# Collez le contenu HTML fourni et sauvegardez

# Éditer style.css
nano style.css
# Collez le contenu CSS fourni et sauvegardez

# Éditer README.md
nano README.md
# Collez le contenu Markdown fourni et sauvegardez
```

### Étape 4 : Premier commit

```bash
# Vérifier l'état
git status
```

**Résultat** :
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        index.html
        style.css
```

```bash
# Ajouter tous les fichiers
git add .
# ou
git add --all
# ou
git add -A

# Vérifier que les fichiers sont staged
git status
```

**Résultat** :
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
        new file:   index.html
        new file:   style.css
```

```bash
# Créer le commit
git commit -m "Initial commit: add basic structure"

# Vérifier l'historique
git log
# ou pour une vue plus compacte
git log --oneline
```

**Résultat** :
```
[main (root-commit) abc1234] Initial commit: add basic structure
 3 files changed, 15 insertions(+)
 create mode 100644 README.md
 create mode 100644 index.html
 create mode 100644 style.css
```

### Étape 5 : Modification et second commit

```bash
# Éditer index.html pour ajouter le paragraphe
nano index.html
# Ajoutez la ligne <p> dans le body

# Éditer style.css pour ajouter le style h1
nano style.css
# Ajoutez les règles CSS pour h1

# Vérifier l'état
git status
```

**Résultat** :
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   style.css
```

```bash
# Ajouter uniquement index.html
git add index.html

# Vérifier
git status
```

**Résultat** :
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   style.css
```

```bash
# Commiter index.html
git commit -m "Add welcome paragraph"

# Ajouter style.css
git add style.css

# Commiter style.css
git commit -m "Add h1 styling"

# Vérifier l'historique final
git log --oneline
```

**Résultat** :
```
def5678 Add h1 styling
abc9012 Add welcome paragraph
abc1234 Initial commit: add basic structure
```

## ✅ Validation finale

```bash
# Vérifier que vous avez 3 commits
git log --oneline
# Devrait montrer 3 lignes

# Vérifier que le dépôt est propre
git status
# Devrait afficher "nothing to commit, working tree clean"

# Vérifier l'existence du dossier .git
ls -la | grep .git
# Devrait montrer le dossier .git
```

## 🎓 Réponses aux questions de réflexion

### 1. Pourquoi avons-nous fait deux commits séparés ?

- **Atomicité** : Chaque commit doit représenter une modification logique unique
- **Traçabilité** : Si le style CSS pose problème, on peut le revert sans toucher au contenu HTML
- **Code review** : Plus facile à relire et comprendre
- **Bonne pratique** : Séparer les changements de contenu des changements de présentation

### 2. Que signifie "working directory clean" ?

- Tous les fichiers ont été committés
- Aucun fichier modifié n'attend dans le working directory
- Aucun fichier dans la staging area
- Le dépôt est à jour et synchronisé avec le dernier commit

### 3. Que contient le dossier `.git` ?

Le dossier `.git` contient toute la mécanique interne de Git :
- **objects/** : Tous les commits, arbres et blobs (versions des fichiers)
- **refs/** : Les références aux branches et tags
- **HEAD** : Pointeur vers le commit actuel
- **config** : Configuration locale du dépôt
- **hooks/** : Scripts automatiques (pre-commit, post-commit, etc.)
- **index** : La staging area (zone de transit)

C'est le "cerveau" de Git qui permet de tracker tout l'historique.

## 📚 Commandes utilisées - Récapitulatif

| Action | Commande |
|--------|----------|
| Initialiser un dépôt | `git init` |
| Voir l'état | `git status` |
| Ajouter des fichiers | `git add <fichier>` ou `git add .` |
| Commiter | `git commit -m "message"` |
| Voir l'historique | `git log` ou `git log --oneline` |
| Voir les fichiers cachés | `ls -la` (Linux/Mac) ou `dir /a` (Windows) |

## 💡 Points clés à retenir

1. **git init** ne se fait qu'une seule fois par projet
2. **git status** est votre meilleur ami - utilisez-le souvent !
3. Un bon message de commit est **descriptif** et **au présent** ("Add" pas "Added")
4. La staging area permet de **contrôler précisément** ce qui sera committé
5. Chaque commit doit être **atomique** et avoir un **objectif précis**

## 🚀 Pour aller plus loin

Essayez ces commandes supplémentaires :

```bash
# Voir les différences avant de commiter
git diff

# Voir l'historique détaillé
git log --stat

# Voir un commit spécifique
git show <commit-id>

# Voir les modifications d'un fichier
git diff index.html
```

---

**Félicitations ! Vous maîtrisez maintenant les bases de Git ! 🎉**

Passez au TP02 pour approfondir la gestion du staging.
