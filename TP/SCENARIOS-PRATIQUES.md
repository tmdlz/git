# Scénarios Pratiques Git - Cas Réels

## 🎯 Introduction

Ces scénarios reproduisent des situations réelles que vous rencontrerez en entreprise. Chaque scénario présente un problème et vous devez le résoudre avec Git.

---

## Scénario 1 : Le Commit Maladroit

### 😰 Situation

Vous venez de commiter sur `main` au lieu de votre branche `feature/login`. Le commit n'a pas encore été pushé.

```bash
# État actuel
(main) $ git log --oneline
abc123 Add login form  # ← Ce commit devrait être sur feature/login !
def456 Update README
```

### 🎯 Objectif

Déplacer le commit `abc123` de `main` vers `feature/login` sans perdre le travail.

### 💡 Indices

- Le commit n'est pas pushé, vous pouvez réécrire l'historique local
- `git cherry-pick` permet de copier un commit
- `git reset` permet de "revenir en arrière"

### ✅ Validation

Après résolution :
- `main` doit être au commit `def456`
- `feature/login` doit contenir le commit du formulaire de login
- Aucun travail ne doit être perdu

---

## Scénario 2 : Conflict Surprise

### 😰 Situation

Vous mergez votre branche `feature/payment` dans `develop`. Git signale un conflit dans `config.js` :

```javascript
<<<<<<< HEAD
const API_URL = 'https://api.prod.example.com';
const TIMEOUT = 5000;
=======
const API_URL = 'https://api.staging.example.com';
const MAX_RETRIES = 3;
>>>>>>> feature/payment
```

### 🎯 Objectif

Résoudre le conflit en gardant :
- L'URL de production (HEAD)
- Le timeout de production (HEAD)
- Le max retries de la feature

### ✅ Résultat attendu

```javascript
const API_URL = 'https://api.prod.example.com';
const TIMEOUT = 5000;
const MAX_RETRIES = 3;
```

---

## Scénario 3 : Le Push Rejeté

### 😰 Situation

```bash
$ git push origin main
To github.com:user/repo.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'origin'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
```

Votre collègue a pushé pendant que vous travailliez.

### 🎯 Objectif

Intégrer ses changements et pousser les vôtres sans perdre de travail.

### 💡 Indices

- `git pull` peut résoudre ça
- Ou `git fetch` + `git rebase` pour un historique plus propre
- Attention aux conflits potentiels

---

## Scénario 4 : Credentials Exposées

### 😰 Situation

Vous avez accidentellement commité vos credentials :

```javascript
// database.js - COMMITÉ IL Y A 2 COMMITS
const DB_PASSWORD = "SuperSecret123!";
const API_KEY = "sk_live_abc123def456";
```

Le commit a déjà été pushé sur GitHub !

### 🎯 Objectif

1. Retirer les credentials de l'historique
2. Remplacer par des variables d'environnement
3. Changer immédiatement les vraies credentials

### ⚠️ Attention

- Réécrire l'historique public = force push nécessaire
- Informer l'équipe AVANT
- Les credentials exposées sont compromises, il faut les changer

### 💡 Solution partielle

```bash
# 1. Modifier l'historique
git rebase -i HEAD~3
# Marquer le commit comme 'edit'

# 2. Modifier le fichier
# database.js
const DB_PASSWORD = process.env.DB_PASSWORD;
const API_KEY = process.env.API_KEY;

# 3. Amend et continue
git add database.js
git commit --amend
git rebase --continue

# 4. Force push (danger!)
git push --force-with-lease
```

---

## Scénario 5 : Les Fichiers Oubliés

### 😰 Situation

Vous avez oublié d'ajouter `package-lock.json` dans votre dernier commit qui ajoutait une dépendance.

```bash
$ git status
On branch feature/api
Changes not staged for commit:
  modified:   package-lock.json
```

Votre dernier commit était "Add axios dependency".

### 🎯 Objectif

Ajouter `package-lock.json` au dernier commit sans créer un nouveau commit.

### 💡 Indices

- `git commit --amend`
- Le commit ne doit PAS avoir été pushé

---

## Scénario 6 : L'Urgence en Plein Dev

### 😰 Situation

Vous êtes en plein développement d'une grosse feature. Vous avez :
- 5 fichiers modifiés
- 2 nouveaux fichiers non-committés
- Des changements à moitié fonctionnels

Votre manager arrive : "Bug critique en prod, il faut corriger MAINTENANT !"

### 🎯 Objectif

1. Sauvegarder votre travail en cours
2. Basculer sur `main`
3. Créer une branche `hotfix/critical-bug`
4. Corriger le bug
5. Revenir à votre feature et récupérer votre travail

### 💡 Outil principal

`git stash` sera votre meilleur ami ici.

---

## Scénario 7 : Le Rebase qui Tourne Mal

### 😰 Situation

Vous rebasez votre feature branch sur `main` :

```bash
$ git rebase main
CONFLICT (content): Merge conflict in app.js
error: could not apply abc1234... Add new feature
```

Après plusieurs tentatives de résolution, vous êtes perdus et voulez juste annuler tout le rebase.

### 🎯 Objectif

Annuler complètement le rebase et revenir à l'état d'avant.

### 💡 Solution

```bash
git rebase --abort
```

---

## Scénario 8 : La Branche Fantôme

### 😰 Situation

Vous avez supprimé une branche localement par erreur :

```bash
$ git branch -D feature/important
Deleted branch feature/important (was abc1234).

$ git checkout feature/important
error: pathspec 'feature/important' did not match any file(s)
```

Mais vous n'aviez pas pushé tous vos commits !

### 🎯 Objectif

Récupérer la branche et tous ses commits.

### 💡 Indices

- `git reflog` garde l'historique de TOUT ce que fait HEAD
- Les commits "supprimés" restent 30 jours minimum
- `git checkout -b` peut créer une branche sur n'importe quel commit

### ✅ Solution

```bash
# Trouver le dernier commit de la branche
git reflog
# abc1234 HEAD@{1}: commit: Last work on feature

# Recréer la branche
git checkout -b feature/important abc1234
```

---

## Scénario 9 : Le Code Review Infernal

### 😰 Situation

Vous avez créé une Pull Request avec 15 commits :
- 5 commits sont "fix typo"
- 3 commits sont "forgot to add file"
- 2 commits sont "work in progress"

Votre reviewer dit : "Peux-tu nettoyer ça avant que je regarde ?"

### 🎯 Objectif

Réorganiser vos commits en 3 commits logiques :
1. "Add user authentication"
2. "Add password validation"
3. "Add tests"

### 💡 Outil

```bash
git rebase -i HEAD~15
```

Dans l'éditeur, utilisez :
- `pick` : garder le commit
- `squash` : fusionner avec le précédent
- `reword` : changer le message
- `drop` : supprimer le commit

---

## Scénario 10 : Le Merge ou le Rebase ?

### 😰 Situation

Votre équipe débat sur la stratégie à utiliser. Vous avez une branche `feature/cart` avec 10 commits. `main` a évolué avec 5 commits.

**Team Merge** dit :
```bash
git checkout feature/cart
git merge main
```

**Team Rebase** dit :
```bash
git checkout feature/cart
git rebase main
```

### 🎯 Question

Quelle est la différence ? Quand utiliser l'un vs l'autre ?

### 💡 Réponse

**git merge** :
- ➕ Préserve l'historique exact
- ➕ Safe pour les branches publiques
- ➖ Crée un commit de merge (historique non-linéaire)
- **Utiliser quand** : Branche partagée, historique important

**git rebase** :
- ➕ Historique linéaire et propre
- ➕ Pas de commit de merge
- ➖ Réécrit l'historique (dangereux si déjà pushé)
- **Utiliser quand** : Feature branch locale, avant de merger dans main

**Règle d'or** :
```
Rebase votre branche locale AVANT de la merger dans main,
Mais ne rebasez JAMAIS des commits déjà pushés et partagés.
```

---

## Scénario 11 : La Recherche du Bug

### 😰 Situation

Un bug est apparu en production. Vous savez qu'il marchait il y a 20 commits. Mais vous ne savez pas QUEL commit l'a cassé.

### 🎯 Objectif

Trouver le commit responsable rapidement.

### 💡 Solution : git bisect

```bash
# Démarrer la recherche binaire
git bisect start

# Marquer l'état actuel comme mauvais
git bisect bad

# Marquer un commit ancien comme bon
git bisect good abc1234

# Git vous place au milieu, testez votre code
# Si ça marche :
git bisect good
# Si ça ne marche pas :
git bisect bad

# Répétez jusqu'à trouver le commit fautif
# Git vous dira : "xyz789 is the first bad commit"

# Terminer
git bisect reset
```

**En 7 tests max**, vous trouverez le coupable parmi 128 commits !

---

## Scénario 12 : Le .gitignore Tardif

### 😰 Situation

Vous avez oublié de créer un `.gitignore` au début. Maintenant vous avez 50 commits et `node_modules/` est versionné (500 MB !).

### 🎯 Objectif

Retirer `node_modules/` de l'historique complet sans perdre le reste.

### 💡 Solution

```bash
# Créer .gitignore
echo "node_modules/" > .gitignore

# Retirer du Git mais garder en local
git rm -r --cached node_modules/

# Commiter
git add .gitignore
git commit -m "Add .gitignore and remove node_modules"

# Pour nettoyer TOUT l'historique (avancé)
git filter-branch --tree-filter 'rm -rf node_modules' HEAD
# ou mieux avec BFG Repo-Cleaner
```

---

## 🎓 Exercice Final : Workflow Complet

### Mission

Simulez un workflow complet de collaboration :

1. **Setup**
   - Créez un repo GitHub "projet-equipe"
   - Clonez-le en local
   - Ajoutez un README

2. **Feature Development**
   - Créez une branche `feature/header`
   - Développez un header HTML/CSS
   - Committez proprement (plusieurs commits logiques)

3. **Sync avec main**
   - Un collègue a pushé sur main (simulez ça)
   - Rebasez votre feature sur main
   - Résolvez les conflits s'il y en a

4. **Pull Request**
   - Pushez votre feature
   - Créez une PR sur GitHub
   - Ajoutez une description détaillée

5. **Code Review**
   - Simulez un commentaire de review
   - Faites les modifications demandées
   - Pushez les changements (la PR se met à jour)

6. **Merge et Cleanup**
   - Mergez la PR
   - En local, revenez sur main
   - Pullez les changements
   - Supprimez la branche feature

### ✅ Validation

À la fin :
- L'historique de main doit être propre
- Aucune branche feature ne doit trainer
- Le projet doit être fonctionnel

---

**Ces scénarios couvrent 90% des situations réelles que vous rencontrerez ! 💪**
