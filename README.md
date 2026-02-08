# 📚 Git & GitHub - Guide Complet pour Débutants

> Un tutoriel complet pour maîtriser Git et GitHub de A à Z

[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)

---

## 📖 Table des Matières

- [Introduction](#-introduction)
- [Installation](#-installation)
- [Concepts Fondamentaux](#-concepts-fondamentaux)
- [Commandes de Base](#-commandes-de-base)
- [Gestion des Branches](#-gestion-des-branches)
- [Collaboration avec GitHub](#-collaboration-avec-github)
- [Commandes Avancées](#-commandes-avancées)
- [Workflows Types](#-workflows-types)
- [Bonnes Pratiques](#-bonnes-pratiques)
- [Ressources](#-ressources)

---

## 🎯 Introduction

### Qu'est-ce que Git ?

**Git** est un système de contrôle de version qui :
- 📝 Enregistre **tous les changements** de vos fichiers
- 🕐 Garde un historique complet (qui, quoi, quand, où)
- 🔄 Permet de revenir à n'importe quelle version précédente
- 👥 Facilite le travail en équipe

### Qu'est-ce que GitHub ?

**GitHub** est une plateforme cloud qui :
- ☁️ Héberge vos dépôts Git en ligne
- 🤝 Permet la collaboration entre développeurs
- 📊 Offre des outils de gestion de projet
- 🌍 Facilite le partage de code open source

> **Analogie** : Git est le café ☕, GitHub est le café où on le sert 🏪

---

## 🔧 Installation

### Windows

```bash
# Télécharger depuis le site officiel
https://git-scm.com/download/win

# Choisir entre 32-bit ou 64-bit
# Utiliser Git Bash après installation
```

### macOS

```bash
# Via Homebrew
brew install git

# Ou via Xcode Command Line Tools
xcode-select --install
```

### Linux

```bash
# Debian/Ubuntu
sudo apt-get install git

# Fedora
sudo dnf install git

# Arch Linux
sudo pacman -S git
```

### Vérification

```bash
git --version
# Devrait afficher : git version 2.x.x
```

---

## 🏗️ Concepts Fondamentaux

### Architecture de Git

```
┌─────────────────────────────────────────────────────────┐
│                    REMOTE REPOSITORY                     │
│                    (GitHub/GitLab)                       │
└─────────────────────────────────────────────────────────┘
                            ▲
                            │ git push
                            │
                            │ git pull/fetch
                            ▼
┌─────────────────────────────────────────────────────────┐
│                   LOCAL REPOSITORY                       │
│                     (.git folder)                        │
└─────────────────────────────────────────────────────────┘
                            ▲
                            │ git commit
                            │
┌─────────────────────────────────────────────────────────┐
│                    STAGING AREA                          │
│                  (Index / Cache)                         │
└─────────────────────────────────────────────────────────┘
                            ▲
                            │ git add
                            │
┌─────────────────────────────────────────────────────────┐
│                  WORKING DIRECTORY                       │
│              (Vos fichiers de projet)                    │
└─────────────────────────────────────────────────────────┘
```

### Les Trois Zones

| Zone | Description | Commande |
|------|-------------|----------|
| **Working Directory** | Votre dossier de travail | - |
| **Staging Area** | Zone de préparation avant commit | `git add` |
| **Repository** | Historique des versions | `git commit` |

---

## 📝 Commandes de Base

### Configuration Initiale (Obligatoire)

```bash
# Configurer votre identité
git config --global user.name "Votre Nom"
git config --global user.email "votre@email.com"

# Vérifier la configuration
git config --list

# Configuration spécifique à un projet (sans --global)
git config user.name "Autre Nom"
```

### Initialiser un Dépôt

```bash
# Créer un nouveau dépôt local
git init

# Cloner un dépôt existant
git clone https://github.com/username/repository.git

# Cloner dans un dossier spécifique
git clone https://github.com/username/repository.git mon-dossier
```

### Suivi des Modifications

```bash
# Voir l'état actuel
git status

# Ajouter des fichiers au staging
git add fichier.txt              # Fichier spécifique
git add .                        # Tout dans le dossier courant
git add -A                       # Tout (même les suppressions)
git add --all                    # Identique à -A
git add *.js                     # Tous les fichiers .js
git add dossier/                 # Tout un dossier

# Commiter les changements
git commit -m "Message descriptif du commit"
git commit -m "feat: ajout authentification utilisateur"

# Add + Commit en une commande (fichiers déjà trackés)
git commit -am "Message"
```

### Historique et Logs

```bash
# Voir l'historique des commits
git log

# Format compact (une ligne par commit)
git log --oneline

# Avec graphique des branches
git log --oneline --graph --all

# Derniers N commits
git log -n 5

# Commits d'un auteur spécifique
git log --author="Nom"

# Commits entre deux dates
git log --since="2024-01-01" --until="2024-12-31"
```

---

## 🌿 Gestion des Branches

### Pourquoi Utiliser des Branches ?

Les branches permettent de :
- ✨ Développer de nouvelles fonctionnalités isolément
- 🐛 Corriger des bugs sans affecter le code principal
- 🧪 Tester des idées sans risque
- 👥 Travailler en parallèle avec d'autres développeurs

### Commandes de Base

```bash
# Lister les branches
git branch                       # Branches locales
git branch -a                    # Toutes les branches (locales + distantes)
git branch -r                    # Branches distantes uniquement

# Créer une branche
git branch nom-branche

# Changer de branche
git checkout nom-branche

# Créer et changer de branche en une commande
git checkout -b nouvelle-branche

# Alternative moderne (Git 2.23+)
git switch nom-branche           # Changer de branche
git switch -c nouvelle-branche   # Créer et changer

# Renommer une branche
git branch -m ancien-nom nouveau-nom

# Supprimer une branche
git branch -d nom-branche        # Suppression sécurisée
git branch -D nom-branche        # Suppression forcée
```

### Fusion de Branches (Merge)

```bash
# Se placer sur la branche de destination
git checkout main

# Fusionner une autre branche
git merge feature-branche

# Annuler un merge en cours
git merge --abort
```

### Gestion des Conflits

Quand Git ne peut pas fusionner automatiquement :

```bash
# 1. Git marque les conflits dans les fichiers
<<<<<<< HEAD
Code de la branche actuelle
=======
Code de la branche à fusionner
>>>>>>> feature-branche

# 2. Éditer manuellement les fichiers
# 3. Résoudre les conflits

# 4. Marquer comme résolu
git add fichier-avec-conflit.txt

# 5. Finaliser le merge
git commit -m "Résolution des conflits"
```

---

## ☁️ Collaboration avec GitHub

### Connexion à un Dépôt Distant

```bash
# Voir les dépôts distants
git remote -v

# Ajouter un dépôt distant
git remote add origin https://github.com/username/repo.git

# Modifier l'URL d'un distant
git remote set-url origin https://github.com/username/nouveau-repo.git

# Supprimer un distant
git remote remove origin
```

### Push (Envoyer vers GitHub)

```bash
# Pousser une branche
git push origin nom-branche

# Pousser et définir le tracking
git push -u origin nom-branche

# Pousser toutes les branches
git push --all origin

# Pousser les tags
git push --tags

# Forcer le push (ATTENTION !)
git push --force                 # ⚠️ À éviter en équipe
```

### Pull & Fetch (Récupérer depuis GitHub)

```bash
# Récupérer ET fusionner
git pull origin main

# Récupérer sans fusionner
git fetch origin

# Après fetch, fusionner manuellement
git merge origin/main

# Pull avec rebase (historique plus propre)
git pull --rebase origin main
```

### Pull Requests (Workflow GitHub)

```bash
# 1. Créer une branche feature
git checkout -b feature/nouvelle-fonctionnalite

# 2. Faire vos modifications et commiter
git add .
git commit -m "feat: ajout nouvelle fonctionnalité"

# 3. Pousser sur GitHub
git push -u origin feature/nouvelle-fonctionnalite

# 4. Sur GitHub :
#    - Aller dans "Pull Requests"
#    - Cliquer "New pull request"
#    - Sélectionner base: main ← compare: feature/nouvelle-fonctionnalite
#    - "Create pull request"
#    - Ajouter titre et description
#    - Assigner des reviewers
#    - Après approbation : "Merge pull request"

# 5. Mettre à jour votre main locale
git checkout main
git pull origin main

# 6. Supprimer la branche feature (optionnel)
git branch -d feature/nouvelle-fonctionnalite
git push origin --delete feature/nouvelle-fonctionnalite
```

---

## 🔥 Commandes Avancées

### Git Stash (Mise de côté temporaire)

```bash
# Mettre de côté les modifications
git stash
git stash save "Message descriptif"

# Voir la liste des stash
git stash list

# Appliquer le dernier stash et le supprimer
git stash pop

# Appliquer sans supprimer
git stash apply

# Appliquer un stash spécifique
git stash apply stash@{2}

# Supprimer un stash
git stash drop stash@{0}

# Supprimer tous les stash
git stash clear

# Créer une branche depuis un stash
git stash branch nouvelle-branche
```

### Git Restore (Annulation)

```bash
# Restaurer un fichier modifié (annuler les changements)
git restore fichier.txt

# Restaurer tous les fichiers
git restore .

# Retirer du staging (unstage)
git restore --staged fichier.txt
git restore --staged .

# Restaurer depuis un commit spécifique
git restore --source=HEAD~2 fichier.txt
```

### Git Reset (Revenir en arrière)

```bash
# Retirer du staging (garder les modifications)
git reset HEAD fichier.txt

# Annuler le dernier commit (garder les modifications)
git reset HEAD~1

# Annuler et SUPPRIMER les modifications
git reset --hard HEAD~1          # ⚠️ DANGEREUX

# Revenir à un commit spécifique
git reset --hard abc123

# Types de reset
git reset --soft HEAD~1          # Garde tout en staging
git reset --mixed HEAD~1         # Garde les modifs (par défaut)
git reset --hard HEAD~1          # Supprime tout
```

### Git Revert (Annuler un commit proprement)

```bash
# Créer un commit inverse
git revert abc123

# Revert sans créer de commit immédiatement
git revert --no-commit abc123

# Revert d'un merge
git revert -m 1 merge-commit-id
```

### Git Rebase (Historique propre)

```bash
# Rebaser la branche actuelle sur main
git checkout feature
git rebase main

# Rebase interactif (modifier l'historique)
git rebase -i HEAD~3

# Options dans le rebase interactif :
# pick   = garder le commit
# reword = modifier le message
# edit   = modifier le commit
# squash = fusionner avec le commit précédent
# drop   = supprimer le commit

# Continuer après résolution de conflits
git rebase --continue

# Annuler le rebase
git rebase --abort
```

⚠️ **ATTENTION** : Ne jamais rebaser des commits déjà poussés sur une branche partagée !

### Git Diff (Comparer)

```bash
# Voir les modifications non stagées
git diff

# Voir les modifications stagées
git diff --staged
git diff --cached

# Comparer deux commits
git diff commit1 commit2

# Comparer deux branches
git diff main..feature

# Voir uniquement les fichiers modifiés
git diff --name-only

# Statistiques de diff
git diff --stat
```

### Git Tag (Versions)

```bash
# Lister les tags
git tag

# Créer un tag léger
git tag v1.0.0

# Créer un tag annoté (recommandé)
git tag -a v1.0.0 -m "Version 1.0.0 - Release initiale"

# Tagger un commit spécifique
git tag -a v1.0.0 abc123

# Pousser un tag
git push origin v1.0.0

# Pousser tous les tags
git push --tags

# Supprimer un tag local
git tag -d v1.0.0

# Supprimer un tag distant
git push origin --delete v1.0.0
```

### Git Cherry-Pick (Appliquer un commit)

```bash
# Appliquer un commit spécifique sur la branche actuelle
git cherry-pick abc123

# Plusieurs commits
git cherry-pick abc123 def456

# Sans créer de commit
git cherry-pick --no-commit abc123
```

---

## 🔄 Workflows Types

### Workflow Feature Branch

```bash
# 1. Mettre à jour main
git checkout main
git pull origin main

# 2. Créer une branche feature
git checkout -b feature/login-system

# 3. Développer
# ... modifications ...
git add .
git commit -m "feat: ajout système de login"

# 4. Pousser régulièrement
git push -u origin feature/login-system

# 5. Mettre à jour depuis main (si nécessaire)
git checkout main
git pull origin main
git checkout feature/login-system
git merge main

# 6. Pull Request sur GitHub

# 7. Après merge, nettoyer
git checkout main
git pull origin main
git branch -d feature/login-system
```

### Workflow Gitflow

```bash
# Branches principales
main           # Production
develop        # Développement

# Branches de support
feature/*      # Nouvelles fonctionnalités
release/*      # Préparation de release
hotfix/*       # Corrections urgentes

# Exemple : Nouvelle fonctionnalité
git checkout develop
git checkout -b feature/new-feature
# ... développement ...
git checkout develop
git merge feature/new-feature
git branch -d feature/new-feature

# Exemple : Release
git checkout develop
git checkout -b release/1.0.0
# ... tests, bug fixes ...
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
git checkout develop
git merge release/1.0.0
git branch -d release/1.0.0

# Exemple : Hotfix
git checkout main
git checkout -b hotfix/critical-bug
# ... fix ...
git checkout main
git merge hotfix/critical-bug
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git checkout develop
git merge hotfix/critical-bug
git branch -d hotfix/critical-bug
```

---

## ✅ Bonnes Pratiques

### Messages de Commit

```bash
# ❌ Mauvais
git commit -m "fix"
git commit -m "update"
git commit -m "blabla"

# ✅ Bon
git commit -m "fix: correction bug affichage profil utilisateur"
git commit -m "feat: ajout système de notifications"
git commit -m "refactor: restructuration des composants React"

# Convention Conventional Commits
feat:     # Nouvelle fonctionnalité
fix:      # Correction de bug
docs:     # Documentation
style:    # Formatage, pas de changement de code
refactor: # Refactorisation
test:     # Ajout de tests
chore:    # Maintenance
```

### .gitignore

```bash
# Créer un fichier .gitignore
touch .gitignore

# Exemples de contenu
# Node.js
node_modules/
npm-debug.log
.env

# Python
__pycache__/
*.py[cod]
venv/
.env

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Fichiers de build
dist/
build/
*.log
```

### Commiter Régulièrement

```bash
# ✅ À FAIRE
- Commiter des modifications logiques et cohérentes
- Commiter souvent (petits commits)
- Tester avant de commiter

# ❌ À ÉVITER
- Gros commits avec trop de changements
- Commiter du code qui ne compile pas
- Commiter des fichiers sensibles (.env, mots de passe)
```

### Travail en Équipe

```bash
# Toujours pull avant de push
git pull origin main
git push origin main

# Communiquer sur les rebase
# Ne jamais rebaser des branches partagées

# Utiliser des Pull Requests
# Faire reviewer son code

# Créer des branches descriptives
feature/user-authentication
bugfix/login-error
hotfix/critical-payment-bug
```

---

## 🛠️ Commandes Utiles

### Nettoyage

```bash
# Supprimer les fichiers non trackés
git clean -n                     # Aperçu
git clean -f                     # Exécution
git clean -fd                    # Fichiers + dossiers

# Supprimer les branches fusionnées
git branch --merged | grep -v "\*" | xargs git branch -d

# Optimiser le dépôt
git gc                           # Garbage collection
git prune                        # Supprimer objets inaccessibles
```

### Recherche

```bash
# Chercher dans les fichiers
git grep "fonction"

# Chercher dans l'historique
git log -S "fonction"

# Qui a modifié cette ligne ?
git blame fichier.txt

# Trouver quel commit a introduit un bug
git bisect start
git bisect bad                   # Commit actuel est mauvais
git bisect good abc123           # Commit abc123 était bon
# Git teste automatiquement les commits intermédiaires
```

### Informations

```bash
# Voir les branches trackées
git branch -vv

# Voir les auteurs et stats
git shortlog -sn

# Taille du dépôt
git count-objects -vH

# Qui a contribué ?
git log --pretty=format:"%an" | sort | uniq -c | sort -rn
```

---

## 📚 Ressources

### Documentation Officielle

- [Git Official](https://git-scm.com/)
- [GitHub Docs](https://docs.github.com/)
- [Git Book (Français)](https://git-scm.com/book/fr/v2)

### Cheat Sheets

- [GitHub Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [Atlassian Git Cheat Sheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

### Outils Visuels

- [GitKraken](https://www.gitkraken.com/) - Client Git visuel
- [Sourcetree](https://www.sourcetreeapp.com/) - Client Git gratuit
- [GitHub Desktop](https://desktop.github.com/) - Client officiel GitHub

### Apprentissage Interactif

- [Learn Git Branching](https://learngitbranching.js.org/?locale=fr_FR) - Tutoriel interactif
- [Git Immersion](https://gitimmersion.com/) - Tour guidé
- [Oh My Git!](https://ohmygit.org/) - Jeu pour apprendre Git

---

## 🎓 Exercices Pratiques

### Exercice 1 : Premier Dépôt

```bash
mkdir mon-projet
cd mon-projet
git init
echo "# Mon Premier Projet" > README.md
git add README.md
git commit -m "Initial commit"
```

### Exercice 2 : Branches

```bash
git checkout -b develop
echo "console.log('Hello');" > app.js
git add app.js
git commit -m "feat: ajout fichier app.js"
git checkout main
git merge develop
```

### Exercice 3 : GitHub

```bash
# Sur GitHub : créer un nouveau dépôt
git remote add origin https://github.com/votre-username/mon-projet.git
git push -u origin main
```

---

## 🆘 Résolution de Problèmes

### Annuler le dernier commit

```bash
# Garder les modifications
git reset --soft HEAD~1

# Supprimer les modifications
git reset --hard HEAD~1
```

### J'ai commité sur la mauvaise branche

```bash
# Annuler le commit
git reset HEAD~ --soft
git stash

# Changer de branche
git checkout bonne-branche
git stash pop
git commit -m "Message"
```

### Synchroniser un fork

```bash
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Supprimer un fichier de l'historique

```bash
# ⚠️ Réécrit l'historique !
git filter-branch --tree-filter 'rm -f fichier-sensible.txt' HEAD
git push --force
```

---

## 📊 Aide-Mémoire Rapide

| Tâche | Commande |
|-------|----------|
| Initialiser | `git init` |
| Cloner | `git clone <url>` |
| État | `git status` |
| Ajouter | `git add .` |
| Commiter | `git commit -m "message"` |
| Pousser | `git push origin main` |
| Tirer | `git pull origin main` |
| Nouvelle branche | `git checkout -b nom` |
| Fusionner | `git merge nom-branche` |
| Historique | `git log --oneline` |
| Annuler modifs | `git restore .` |
| Stash | `git stash` / `git stash pop` |

---

## 🤝 Contribution

Ce guide est basé sur le tutoriel de **Sumit Saha** et est destiné à l'apprentissage de Git et GitHub.

---

## 📄 Licence

Ce document est libre d'utilisation à des fins éducatives.

---

## 🎯 Conclusion

Git est un outil **essentiel** pour tout développeur. Une fois maîtrisé, il vous accompagnera tout au long de votre carrière.

**Prochaines étapes** :
1. ✅ Pratiquer les commandes de base quotidiennement
2. ✅ Créer des projets sur GitHub
3. ✅ Contribuer à des projets open source
4. ✅ Approfondir avec Git Hooks, Submodules, etc.

---

**Bon apprentissage ! 🚀**
