# Index des Fichiers - TP Git & GitHub

## 📚 Structure Complète du Parcours

```
git-tp/
├── README.md                          # Introduction et présentation générale
│
├── GIT-CHEAT-SHEET.md                 # Guide de référence rapide de toutes les commandes
│
├── BONNES-PRATIQUES.md                # Guide des bonnes pratiques professionnelles
│
├── SCENARIOS-PRATIQUES.md             # Situations réelles et comment les résoudre
│
├── TP01-initialisation-commits.md     # TP sur l'initialisation et premiers commits
├── TP01-REPONSES.md                   # Solutions détaillées du TP01
│
├── TP02-staging-avance.md             # TP sur la gestion avancée du staging
├── TP02-REPONSES.md                   # Solutions détaillées du TP02
│
├── TP03-historique-navigation.md      # TP sur la navigation dans l'historique
├── TP03-REPONSES.md                   # Solutions détaillées du TP03
│
├── TP04-05-06-branches-merge-github.md # TP04: Branches, TP05: Merge, TP06: GitHub
│
└── TP07-08-09-10-avance.md            # TP07-10: Stash, Revert, Rebase, Pull Requests
```

## 🎯 Parcours Recommandé

### Niveau Débutant (Jours 1-3)

1. **Lire** : `README.md`
2. **Pratiquer** : 
   - `TP01-initialisation-commits.md`
   - `TP02-staging-avance.md`
3. **Référence** : `GIT-CHEAT-SHEET.md` (section Configuration & Commits)

### Niveau Intermédiaire (Jours 4-7)

1. **Pratiquer** :
   - `TP03-historique-navigation.md`
   - `TP04-05-06-branches-merge-github.md` (TP04 et TP05)
2. **Lire** : `BONNES-PRATIQUES.md` (sections 1-4)
3. **Référence** : `GIT-CHEAT-SHEET.md` (section Branches & Merge)

### Niveau Avancé (Jours 8-10)

1. **Pratiquer** :
   - `TP04-05-06-branches-merge-github.md` (TP06)
   - `TP07-08-09-10-avance.md`
2. **Lire** : `BONNES-PRATIQUES.md` (sections 5-8)
3. **Défis** : `SCENARIOS-PRATIQUES.md`

### Maîtrise (Semaine 2+)

1. **Exercice final** : `SCENARIOS-PRATIQUES.md` - Exercice Final
2. **Référence permanente** : `GIT-CHEAT-SHEET.md`
3. **Standards professionnels** : `BONNES-PRATIQUES.md`

## 📖 Description des Fichiers

### README.md
- Introduction au parcours
- Objectifs pédagogiques
- Prérequis et configuration
- Structure des TP
- Conseils d'utilisation

### GIT-CHEAT-SHEET.md
**Contenu** :
- Configuration initiale
- Création de dépôt
- Staging et commits
- Historique et navigation
- Branches et merge
- Rebase
- Stash
- Remote (push/pull/fetch)
- Tags
- Nettoyage
- Workflows courants
- Alias utiles
- Situations d'urgence

**Utilisation** : Référence rapide à garder sous la main

### BONNES-PRATIQUES.md
**Contenu** :
1. Messages de commit (conventions, exemples)
2. Organisation des branches (Git Flow, GitHub Flow)
3. Workflow de développement (feature branch, commits atomiques)
4. Code review (pour reviewer et auteur)
5. Sécurité (secrets, .gitignore)
6. Performance (optimisation du repo)
7. Collaboration (communication, conventions)
8. Erreurs à éviter (top 10 + solutions)

**Utilisation** : Guide à lire et à appliquer en équipe

### SCENARIOS-PRATIQUES.md
**Contenu** :
12 scénarios réels :
1. Commit sur mauvaise branche
2. Conflits de merge
3. Push rejeté
4. Credentials exposées
5. Fichiers oubliés
6. Urgence en plein dev
7. Rebase qui échoue
8. Branche supprimée par erreur
9. Historique à nettoyer
10. Merge vs Rebase (décision)
11. Recherche de bug (bisect)
12. .gitignore tardif
+ Exercice final complet

**Utilisation** : Entraînement pratique, simulations de problèmes réels

### TP01 - Initialisation et Premiers Commits
**Objectifs** :
- Initialiser un dépôt Git
- Créer et modifier des fichiers
- Utiliser git status, git add, git commit
- Comprendre le workflow de base

**Durée estimée** : 45 minutes

### TP02 - Gestion Avancée du Staging
**Objectifs** :
- Maîtriser git add (., -A, *, patterns)
- Unstager des fichiers
- Gérer les suppressions (git rm)
- Staging sélectif

**Durée estimée** : 1 heure

### TP03 - Navigation dans l'Historique
**Objectifs** :
- Utiliser git log avec options
- Comparer des commits (git diff)
- Voyager dans le temps (git checkout)
- Comprendre detached HEAD
- Examiner des commits spécifiques

**Durée estimée** : 1h15

### TP04 - Branching et Workflow
**Objectifs** :
- Créer et gérer des branches
- Basculer entre branches
- Comprendre le workflow feature branch
- Développer en parallèle

**Durée estimée** : 1 heure

### TP05 - Merge et Conflits
**Objectifs** :
- Merger des branches
- Créer et résoudre des conflits
- Fast-forward vs merge commit
- Conflits multi-fichiers

**Durée estimée** : 1h30

### TP06 - Collaboration GitHub
**Objectifs** :
- Créer un dépôt GitHub
- Push/Pull/Fetch
- Cloner un dépôt
- Synchroniser local et remote
- Gérer les branches distantes

**Durée estimée** : 1h15

### TP07 - Git Stash
**Objectifs** :
- Sauvegarder temporairement du travail
- Stash pop vs apply
- Gérer plusieurs stashes
- Cas d'usage pratiques

**Durée estimée** : 45 minutes

### TP08 - Git Revert
**Objectifs** :
- Annuler des commits proprement
- Revert vs Reset
- Gérer les reverts en cascade
- Résoudre conflits de revert

**Durée estimée** : 1 heure

### TP09 - Git Rebase
**Objectifs** :
- Comprendre et utiliser rebase
- Nettoyer l'historique
- Rebase vs merge
- Rebase interactif
- Gérer les conflits

**Durée estimée** : 1h30

### TP10 - Pull Requests
**Objectifs** :
- Créer une Pull Request
- Faire du code review
- Gérer commentaires et modifications
- Merger une PR
- Workflow complet de collaboration

**Durée estimée** : 1h45

## 🎯 Temps Total Estimé

- **Niveau Débutant** : 8-10 heures
- **Niveau Intermédiaire** : 12-15 heures
- **Niveau Avancé** : 18-22 heures
- **Maîtrise** : 25-30 heures

## 💡 Conseils d'Utilisation

### Pour apprendre efficacement

1. **Ne sautez pas les étapes** : Chaque TP construit sur le précédent
2. **Pratiquez avant de lire les réponses** : C'est essentiel !
3. **Faites les TP plusieurs fois** : La répétition est clé
4. **Expérimentez** : Git permet de revenir en arrière
5. **Gardez le cheat sheet ouvert** : C'est normal de chercher

### Pour les formateurs

Ces ressources peuvent être utilisées pour :
- Formation Git sur 2-3 jours (intensif)
- Formation Git sur 2 semaines (normal)
- Auto-formation guidée
- Exercices pratiques en cours
- Évaluations (les TP sans réponses)

### Pour les équipes

- `BONNES-PRATIQUES.md` → À adapter et adopter comme standard d'équipe
- `SCENARIOS-PRATIQUES.md` → Base de quiz technique pour recrutement
- Les TP → Onboarding des nouveaux développeurs

## 📊 Progression Suggérée

```
Semaine 1
├── Jour 1: Setup + TP01
├── Jour 2: TP02
├── Jour 3: TP03
├── Jour 4: TP04
└── Jour 5: TP05

Semaine 2
├── Jour 1: TP06
├── Jour 2: TP07 + TP08
├── Jour 3: TP09
├── Jour 4: TP10
└── Jour 5: Scénarios pratiques
```

## 🏆 Certification Personnelle

Une fois tous les TP terminés :
- [ ] Tous les TP (01-10) complétés sans regarder les réponses
- [ ] Tous les scénarios pratiques résolus
- [ ] Cheat sheet lu et compris
- [ ] Bonnes pratiques lues et intégrées
- [ ] Projet personnel versionné avec Git
- [ ] Au moins 1 Pull Request créée et mergée

**→ Vous êtes prêt pour utiliser Git professionnellement ! 🎉**

## 🔗 Ressources Complémentaires

### Officielles
- [Documentation Git](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/fr/v2) (gratuit)
- [GitHub Guides](https://guides.github.com/)

### Interactives
- [Learn Git Branching](https://learngitbranching.js.org/?locale=fr_FR)
- [Git Exercises](https://gitexercises.fracz.com/)
- [Oh My Git!](https://ohmygit.org/) (jeu)

### Outils
- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) (VSCode)
- [GitKraken](https://www.gitkraken.com/) (GUI)
- [Sourcetree](https://www.sourcetreeapp.com/) (GUI)

---

**Bon apprentissage ! N'oubliez pas : la meilleure façon d'apprendre Git, c'est de pratiquer ! 💪**
