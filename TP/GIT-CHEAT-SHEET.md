# Git Cheat Sheet - Guide de Référence Rapide

## 🎯 Configuration Initiale

```bash
# Configurer votre identité (obligatoire pour le premier commit)
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"

# Vérifier la configuration
git config --list
git config user.name

# Configuration locale (pour un projet spécifique)
git config --local user.name "Autre Nom"

# Définir l'éditeur par défaut
git config --global core.editor "code --wait"  # VSCode
git config --global core.editor "nano"          # Nano
```

---

## 📁 Création de Dépôt

```bash
# Initialiser un nouveau dépôt local
git init

# Cloner un dépôt distant
git clone <url>
git clone <url> <nom-dossier>

# Cloner une branche spécifique
git clone -b <branche> <url>
```

---

## 📊 Vérifier l'État

```bash
# État actuel du dépôt
git status

# Version courte
git status -s

# Voir les différences non stagées
git diff

# Voir les différences stagées
git diff --staged
git diff --cached

# Différence entre deux commits
git diff <commit1> <commit2>

# Différence sur un fichier spécifique
git diff <fichier>
```

---

## ➕ Staging (Zone de Transit)

```bash
# Ajouter un fichier spécifique
git add <fichier>

# Ajouter tous les fichiers du dossier courant
git add .

# Ajouter tous les fichiers du dépôt
git add -A
git add --all

# Ajouter par pattern
git add *.js
git add src/

# Ajouter interactivement (choisir ce qu'on veut)
git add -p

# Unstage un fichier
git restore --staged <fichier>
git reset HEAD <fichier>  # ancienne méthode

# Unstage tout
git restore --staged .
git reset HEAD
```

---

## 💾 Commit

```bash
# Créer un commit
git commit -m "Message du commit"

# Commit avec description longue
git commit -m "Titre" -m "Description détaillée"

# Ajouter et commiter en une commande (fichiers déjà trackés)
git commit -am "Message"

# Modifier le dernier commit (message ou contenu)
git commit --amend -m "Nouveau message"

# Ajouter des fichiers au dernier commit sans changer le message
git add <fichier>
git commit --amend --no-edit
```

---

## 📜 Historique

```bash
# Voir l'historique complet
git log

# Historique compact (une ligne par commit)
git log --oneline

# Historique avec graphe
git log --graph --oneline --all

# Historique avec statistiques
git log --stat

# Historique d'un fichier spécifique
git log <fichier>
git log --follow <fichier>  # suit les renommages

# N derniers commits
git log -n 5
git log -5

# Commits entre deux dates
git log --since="2024-01-01" --until="2024-12-31"

# Commits par auteur
git log --author="John"

# Rechercher dans les messages
git log --grep="fix"

# Voir un commit spécifique
git show <commit-id>

# Qui a modifié chaque ligne d'un fichier
git blame <fichier>
```

---

## 🌿 Branches

```bash
# Lister les branches locales
git branch

# Lister toutes les branches (local + remote)
git branch -a

# Lister les branches avec dernier commit
git branch -v

# Créer une nouvelle branche
git branch <nom-branche>

# Basculer sur une branche
git checkout <branche>
git switch <branche>  # nouvelle syntaxe

# Créer et basculer en une commande
git checkout -b <nouvelle-branche>
git switch -c <nouvelle-branche>

# Renommer une branche
git branch -m <ancien-nom> <nouveau-nom>
git branch -m <nouveau-nom>  # branche courante

# Supprimer une branche locale
git branch -d <branche>   # sécurisé (vérifie si mergée)
git branch -D <branche>   # force

# Supprimer une branche distante
git push origin --delete <branche>

# Voir les branches mergées
git branch --merged
git branch --no-merged
```

---

## 🔀 Merge (Fusion)

```bash
# Merger une branche dans la branche courante
git merge <branche>

# Merge avec message personnalisé
git merge <branche> -m "Message de merge"

# Forcer un merge commit (pas de fast-forward)
git merge <branche> --no-ff

# Annuler un merge en cours
git merge --abort

# Voir les conflits
git diff --name-only --diff-filter=U

# Après résolution des conflits
git add <fichiers-résolus>
git commit
```

---

## 🔄 Rebase

```bash
# Rebaser la branche courante sur une autre
git rebase <branche>

# Rebase interactif (pour réorganiser/fusionner commits)
git rebase -i HEAD~3  # 3 derniers commits

# Continuer après résolution de conflit
git add <fichiers>
git rebase --continue

# Annuler un rebase
git rebase --abort

# Ignorer un commit pendant le rebase
git rebase --skip
```

---

## ↩️ Annuler des Changements

```bash
# Annuler les modifications dans un fichier (pas encore stagé)
git restore <fichier>
git checkout -- <fichier>  # ancienne méthode

# Annuler toutes les modifications non stagées
git restore .

# Annuler le dernier commit (garde les changements en working directory)
git reset HEAD~1
git reset --soft HEAD~1

# Annuler le dernier commit (supprime les changements)
git reset --hard HEAD~1

# Retourner à un commit spécifique
git reset --hard <commit-id>

# Créer un commit qui annule un commit précédent (safe pour remote)
git revert <commit-id>

# Revert sans créer de commit immédiatement
git revert <commit-id> --no-commit
```

---

## 💼 Stash (Sauvegarde Temporaire)

```bash
# Sauvegarder les modifications en cours
git stash
git stash save "Message descriptif"

# Lister les stashes
git stash list

# Appliquer le dernier stash (et le supprimer)
git stash pop

# Appliquer le dernier stash (sans le supprimer)
git stash apply

# Appliquer un stash spécifique
git stash apply stash@{2}
git stash pop stash@{2}

# Voir le contenu d'un stash
git stash show
git stash show -p  # avec les différences

# Supprimer un stash
git stash drop stash@{0}

# Supprimer tous les stashes
git stash clear

# Stasher uniquement les fichiers trackés
git stash --keep-index

# Stasher aussi les fichiers non-trackés
git stash -u
git stash --include-untracked
```

---

## 🗑️ Suppression de Fichiers

```bash
# Supprimer un fichier (du Git et du système)
git rm <fichier>

# Supprimer du Git mais garder en local
git rm --cached <fichier>

# Supprimer un dossier récursivement
git rm -r <dossier>

# Forcer la suppression (fichier modifié)
git rm -f <fichier>
```

---

## 🌐 Remote (Dépôt Distant)

```bash
# Ajouter un remote
git remote add origin <url>

# Voir les remotes configurés
git remote -v

# Renommer un remote
git remote rename origin upstream

# Supprimer un remote
git remote remove origin

# Voir les infos d'un remote
git remote show origin

# Changer l'URL d'un remote
git remote set-url origin <nouvelle-url>
```

---

## ⬆️ Push (Envoyer vers Remote)

```bash
# Pousser vers le remote
git push origin <branche>

# Premier push d'une branche (configure le tracking)
git push -u origin <branche>
git push --set-upstream origin <branche>

# Pousser toutes les branches
git push origin --all

# Pousser les tags
git push origin --tags

# Forcer un push (DANGER - écrase l'historique distant)
git push --force
git push -f

# Force push plus sûr (refuse si des commits ont été ajoutés)
git push --force-with-lease

# Supprimer une branche distante
git push origin --delete <branche>
```

---

## ⬇️ Pull / Fetch (Récupérer depuis Remote)

```bash
# Récupérer ET merger les changements
git pull origin <branche>

# Pull avec rebase au lieu de merge
git pull --rebase origin <branche>

# Récupérer les changements SANS merger
git fetch origin

# Fetch toutes les branches
git fetch --all

# Fetch et supprimer les branches qui n'existent plus sur remote
git fetch --prune
git fetch -p

# Voir les différences avec le remote
git diff origin/main
```

---

## 🏷️ Tags

```bash
# Lister les tags
git tag

# Créer un tag léger
git tag v1.0.0

# Créer un tag annoté (recommandé)
git tag -a v1.0.0 -m "Version 1.0.0"

# Tagger un commit spécifique
git tag -a v1.0.0 <commit-id> -m "Message"

# Voir les infos d'un tag
git show v1.0.0

# Pousser un tag
git push origin v1.0.0

# Pousser tous les tags
git push origin --tags

# Supprimer un tag local
git tag -d v1.0.0

# Supprimer un tag distant
git push origin --delete v1.0.0

# Checkout un tag
git checkout v1.0.0
```

---

## 🔍 Recherche

```bash
# Rechercher dans les fichiers
git grep "texte"

# Rechercher dans un commit spécifique
git grep "texte" <commit-id>

# Rechercher dans tous les commits
git log -S "texte"

# Rechercher dans les messages de commit
git log --grep="bug fix"
```

---

## 🧹 Nettoyage

```bash
# Supprimer les fichiers non-trackés (dry-run d'abord)
git clean -n

# Supprimer les fichiers non-trackés
git clean -f

# Supprimer aussi les dossiers
git clean -fd

# Supprimer aussi les fichiers ignorés
git clean -fdx

# Optimiser le dépôt (garbage collection)
git gc

# Vérifier l'intégrité du dépôt
git fsck
```

---

## 🎯 Workflows Courants

### Workflow Feature Branch

```bash
# 1. Créer une feature branch depuis main
git checkout main
git pull origin main
git checkout -b feature/nouvelle-fonctionnalite

# 2. Développer et commiter
git add .
git commit -m "Add new feature"

# 3. Pousser la feature
git push -u origin feature/nouvelle-fonctionnalite

# 4. Créer une Pull Request sur GitHub

# 5. Après merge, nettoyer
git checkout main
git pull origin main
git branch -d feature/nouvelle-fonctionnalite
```

### Workflow Hotfix

```bash
# 1. Créer depuis main
git checkout main
git pull origin main
git checkout -b hotfix/bug-critique

# 2. Corriger et tester
git add .
git commit -m "Fix critical bug"

# 3. Merger directement
git checkout main
git merge hotfix/bug-critique
git push origin main

# 4. Nettoyer
git branch -d hotfix/bug-critique
```

### Synchroniser avec Remote

```bash
# Récupérer les updates et rebaser
git fetch origin
git rebase origin/main

# Ou en une commande
git pull --rebase origin main
```

---

## ⚙️ Alias Utiles

```bash
# Créer des alias pour gagner du temps
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'restore --staged'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'
git config --global alias.amend 'commit --amend --no-edit'

# Utilisation
git co main      # au lieu de git checkout main
git st           # au lieu de git status
git visual       # graphe visuel
```

---

## 🆘 Situations d'Urgence

### J'ai committé sur la mauvaise branche

```bash
# Sauvegarder le commit
git log  # noter le commit-id

# Annuler le commit sur la branche actuelle
git reset --hard HEAD~1

# Aller sur la bonne branche
git checkout bonne-branche

# Appliquer le commit
git cherry-pick <commit-id>
```

### J'ai pushé des credentials

```bash
# NE PAS faire un simple commit de correction
# Refaire l'historique
git rebase -i HEAD~n  # n = nombre de commits en arrière

# Dans l'éditeur, marquer 'edit' le commit problématique
# Modifier le fichier
git add .
git commit --amend
git rebase --continue

# Force push
git push --force-with-lease

# PUIS changer immédiatement les credentials !
```

### Récupérer un commit "perdu"

```bash
# Git garde tout pendant ~30 jours
git reflog  # voir tous les mouvements de HEAD

# Récupérer
git checkout <commit-id-du-reflog>
git checkout -b branche-de-recuperation
```

---

## 📝 Bonnes Pratiques

### Messages de Commit

```
feat: Add user authentication
fix: Correct calculation in total price
docs: Update README with installation steps
style: Format code according to style guide
refactor: Restructure database queries
test: Add unit tests for login
chore: Update dependencies
```

### Avant de Commiter

```bash
# Toujours vérifier ce qu'on commit
git status
git diff
git diff --staged

# Séparer les changements logiques
git add -p  # ajouter par morceaux
```

### Avant de Merger/Rebaser

```bash
# S'assurer d'être à jour
git fetch origin
git status

# Faire un backup de sécurité
git branch backup-avant-rebase
```

---

## 🚫 À NE JAMAIS FAIRE

❌ `git push --force` sur une branche partagée  
❌ Rebase de commits déjà pushés et utilisés par d'autres  
❌ Commiter des mots de passe ou clés API  
❌ Faire des commits massifs (300+ fichiers)  
❌ Utiliser `git reset --hard` sans comprendre  

---

**💡 Astuce** : En cas de doute, créez une branche de backup avant toute manipulation risquée !
