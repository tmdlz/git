# Git & GitHub - Guide Complet

## 🎯 Qu'est-ce que Git et GitHub ?

**Git** = L'outil de versionnage (le café ☕)  
**GitHub** = La plateforme en ligne pour stocker vos projets (le café où on le sert 🏪)

Git enregistre **tous les changements** de vos fichiers : quoi, quand, qui, où.

---

## 📁 Architecture de Git

### Les 3 zones principales

1. **Working Directory** (Répertoire de travail)
   - Votre dossier de projet local
   - Là où vous créez/modifiez vos fichiers

2. **Staging Area** (Zone de transit)
   - Espace intermédiaire avant la sauvegarde définitive
   - Permet de réviser avant de "commiter"

3. **Repository** (Dépôt)
   - **Local** : sur votre machine
   - **Remote** : sur GitHub (cloud)

```
Working Directory → Staging Area → Local Repository → Remote Repository
      (git add)         (git commit)        (git push)
```

---

## 🚀 Installation et Configuration

### Installation
```bash
# Vérifier l'installation
git --version
```

### Configuration initiale (obligatoire)
```bash
git config --global user.email "votre@email.com"
git config --global user.name "Votre Nom"
```

---

## 📝 Commandes Essentielles

### Initialisation
```bash
# Créer un nouveau dépôt local
git init

# Cloner un dépôt distant
git clone <url>
```

### Suivi des modifications
```bash
# Voir l'état des fichiers
git status

# Ajouter des fichiers au staging
git add .                    # Tout ajouter
git add <fichier>            # Fichier spécifique
git add *.txt                # Par extension

# Commiter (sauvegarder)
git commit -m "Message descriptif"
```

### Historique
```bash
# Voir l'historique des commits
git log
git log --oneline           # Version compacte
```

### Annulation
```bash
# Retirer du staging (sans perdre les modifications)
git reset

# Restaurer un fichier à son dernier commit
git restore <fichier>
git restore .               # Tout restaurer

# Annuler un commit (crée un nouveau commit inverse)
git revert <commit-id>
```

---

## 🌿 Branches

Les branches permettent de travailler sur des fonctionnalités séparément.

```bash
# Lister les branches
git branch

# Créer une branche
git branch <nom-branche>

# Changer de branche
git checkout <nom-branche>

# Créer et changer de branche en une commande
git checkout -b <nom-branche>

# Fusionner une branche dans la branche actuelle
git merge <nom-branche>
```

### Gestion des conflits de merge
Quand deux branches modifient la même ligne :
1. Git marque le conflit dans le fichier
2. Vous éditez manuellement pour garder la bonne version
3. `git add` + `git commit` pour finaliser

---

## ☁️ Synchronisation avec GitHub

### Push (envoyer vers le remote)
```bash
git push origin <nom-branche>
git push origin main
```

### Fetch & Pull (récupérer depuis le remote)
```bash
# Télécharger sans fusionner
git fetch

# Télécharger ET fusionner
git pull                    # = fetch + merge
```

---

## 💾 Commandes Avancées

### Git Stash (sauvegarder temporairement)
Utile quand vous devez changer de branche sans commiter.

```bash
# Mettre de côté les modifications
git stash

# Récupérer ET supprimer du stash
git stash pop

# Récupérer SANS supprimer du stash
git stash apply

# Voir la liste des stash
git stash list

# Supprimer un stash
git stash drop
```

### Git Rebase
Alternative au merge pour un historique plus propre.

```bash
# Rebaser la branche actuelle sur main
git rebase main
```

⚠️ **Ne jamais rebaser des branches publiques/partagées !**

### Comparaison entre commits
```bash
git diff <commit-id-1> <commit-id-2>
```

---

## 🔄 Pull Requests (GitHub)

Processus pour proposer des modifications :

1. Créer une branche et faire vos modifications
2. Pusher la branche sur GitHub
3. Sur GitHub : **Pull Requests** → **New pull request**
4. Sélectionner la branche source et destination
5. **Create pull request**
6. Après review : **Merge pull request**

---

## 🎯 Workflow Type

```bash
# 1. Cloner ou initialiser
git clone <url>

# 2. Créer une branche pour votre feature
git checkout -b feature/nouvelle-fonctionnalite

# 3. Travailler et commiter régulièrement
git add .
git commit -m "Ajout de la fonctionnalité X"

# 4. Pousser sur GitHub
git push origin feature/nouvelle-fonctionnalite

# 5. Créer une Pull Request sur GitHub

# 6. Après merge, mettre à jour main localement
git checkout main
git pull
```

---

## 🛠️ Commandes de Suppression

```bash
# Supprimer un fichier + stage la suppression
git rm <fichier>

# Supprimer de force (même si modifié)
git rm -f <fichier>

# Retirer du staging mais garder le fichier
git rm --cached <fichier>

# Supprimer un dossier récursivement
git rm -r <dossier>
```

---

## 📊 Résumé des Différences

| Commande | Action |
|----------|--------|
| `git reset` | Annule le staging (changements restent) |
| `git restore` | Annule les modifications non commitées |
| `git revert` | Annule un commit (crée un nouveau commit) |
| `git stash pop` | Récupère + supprime du stash |
| `git stash apply` | Récupère sans supprimer du stash |
| `git merge` | Fusionne avec commit de merge |
| `git rebase` | Fusionne sans commit de merge (historique linéaire) |

---

## 💡 Bonnes Pratiques

✅ **À FAIRE**
- Commiter souvent avec des messages clairs
- Créer une branche par fonctionnalité
- Tirer (`pull`) avant de pousser (`push`)
- Vérifier avec `git status` régulièrement

❌ **À ÉVITER**
- Commiter directement sur `main` en équipe
- Messages de commit vagues ("fix", "update")
- Rebase sur des branches partagées
- Oublier de `pull` avant de commencer à travailler

---

## 🔗 Ressources

- [Cheat Sheet Git](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [Documentation officielle](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)

---

**Créé par Linus Torvalds** (le créateur de Linux) 🐧

> Git est un outil que vous utiliserez toute votre carrière de développeur !
