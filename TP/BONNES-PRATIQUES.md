# Guide des Bonnes Pratiques Git

## 📋 Table des matières

1. [Messages de Commit](#messages-de-commit)
2. [Organisation des Branches](#organisation-des-branches)
3. [Workflow de Développement](#workflow-de-développement)
4. [Code Review](#code-review)
5. [Sécurité](#sécurité)
6. [Performance](#performance)
7. [Collaboration](#collaboration)
8. [Erreurs à Éviter](#erreurs-à-éviter)

---

## 1. Messages de Commit

### ✅ Structure d'un bon message

```
<type>(<scope>): <sujet>

<corps optionnel>

<footer optionnel>
```

### Types conventionnels

| Type | Utilisation | Exemple |
|------|-------------|---------|
| `feat` | Nouvelle fonctionnalité | `feat(auth): add login with Google` |
| `fix` | Correction de bug | `fix(cart): correct total calculation` |
| `docs` | Documentation | `docs(readme): add installation steps` |
| `style` | Formatage, pas de changement de code | `style: format with prettier` |
| `refactor` | Refactoring | `refactor(api): simplify error handling` |
| `test` | Ajout de tests | `test(user): add unit tests for registration` |
| `chore` | Maintenance, dépendances | `chore: update dependencies` |
| `perf` | Amélioration de performance | `perf(db): optimize query execution` |
| `ci` | CI/CD | `ci: add GitHub Actions workflow` |
| `build` | Build system | `build: update webpack config` |
| `revert` | Annulation d'un commit | `revert: feat(auth): add login with Google` |

### 📝 Règles d'or

**DO** ✅
```bash
git commit -m "feat(user): add email validation on registration"
git commit -m "fix(api): handle null response from external service"
git commit -m "docs: update README with new environment variables"
```

**DON'T** ❌
```bash
git commit -m "fixes"
git commit -m "update stuff"
git commit -m "WIP"
git commit -m "aaaaaah finally it works!!!"
```

### 📏 Longueur et format

- **Sujet** : Max 50 caractères
- **Corps** : Max 72 caractères par ligne
- **Impératif présent** : "Add feature" pas "Added feature"
- **Pas de point final** dans le sujet

### 📖 Exemple complet

```bash
git commit -m "feat(payment): integrate Stripe payment gateway

- Add Stripe SDK dependency
- Create payment service with card tokenization
- Implement webhook for payment confirmation
- Add error handling for failed transactions

Closes #123
See: https://stripe.com/docs/payments"
```

---

## 2. Organisation des Branches

### 🌳 Git Flow (recommandé pour projets moyens/grands)

```
main (production)
  └── develop (développement)
       ├── feature/user-auth
       ├── feature/shopping-cart
       └── release/v1.2.0
  └── hotfix/critical-bug
```

**Branches permanentes** :
- `main` : Code en production
- `develop` : Prochaine version en développement

**Branches temporaires** :
- `feature/*` : Nouvelles fonctionnalités
- `hotfix/*` : Corrections urgentes sur production
- `release/*` : Préparation d'une release
- `bugfix/*` : Corrections de bugs

### 🚀 GitHub Flow (recommandé pour projets simples)

```
main
  ├── feature/add-login
  ├── feature/redesign-homepage
  └── fix/navbar-mobile
```

**Plus simple** :
- `main` : Toujours déployable
- `feature/*` : Tout le reste

### 📛 Conventions de nommage

```bash
# Feature
feature/nom-de-la-feature
feature/user-authentication
feature/payment-integration

# Fix
fix/nom-du-bug
fix/login-redirect
hotfix/critical-memory-leak

# Release
release/v1.2.0
release/2024-Q1

# Autres
docs/api-documentation
refactor/database-layer
test/integration-tests
```

**Règles** :
- Tout en minuscules
- Mots séparés par des tirets (kebab-case)
- Descriptif et court
- Pas d'accents ou caractères spéciaux

---

## 3. Workflow de Développement

### 🔄 Workflow Feature Branch

```bash
# 1. Toujours partir de main à jour
git checkout main
git pull origin main

# 2. Créer la feature branch
git checkout -b feature/user-profile

# 3. Développer et commiter régulièrement
# ... modifications ...
git add .
git commit -m "feat(profile): add basic profile page"
# ... plus de modifications ...
git add .
git commit -m "feat(profile): add avatar upload"

# 4. Synchroniser avec main régulièrement
git fetch origin
git rebase origin/main
# ou
git merge origin/main

# 5. Pousser la branche
git push -u origin feature/user-profile

# 6. Créer une Pull Request sur GitHub

# 7. Après review et merge, cleanup
git checkout main
git pull origin main
git branch -d feature/user-profile
git remote prune origin
```

### 📏 Taille des commits

**Atomic commits** : Un commit = Une modification logique

✅ **BON**
```bash
# Commit 1
git commit -m "feat(auth): add login form UI"

# Commit 2
git commit -m "feat(auth): add login validation"

# Commit 3
git commit -m "feat(auth): add login API integration"
```

❌ **MAUVAIS**
```bash
# Un énorme commit
git commit -m "feat(auth): add complete authentication system"
# Contient : UI + validation + API + tests + doc
```

### 🧹 Nettoyer avant merge

```bash
# Squash les petits commits
git rebase -i HEAD~5

# Dans l'éditeur :
pick abc1234 feat(auth): add login form
squash def5678 fix: typo in login form
squash ghi9012 fix: another typo
pick jkl3456 feat(auth): add validation
squash mno7890 fix: validation error message

# Résultat : 2 commits propres au lieu de 5
```

---

## 4. Code Review

### 👀 Pour le reviewer

**Checklist de review** :
- [ ] Le code fait ce qu'il dit
- [ ] Les tests passent
- [ ] Pas de code mort (commenté)
- [ ] Pas de credentials ou secrets
- [ ] Conformité au style du projet
- [ ] Documentation à jour si nécessaire
- [ ] Performance acceptable

**Ton des commentaires** :

✅ **BON**
```
💡 Suggestion: On pourrait extraire cette logique dans une fonction séparée 
pour améliorer la lisibilité.

⚠️ Attention: Cette requête pourrait être optimisée avec un index sur user_id.

❓ Question: Pourquoi utiliser setTimeout ici plutôt qu'un Promise ?
```

❌ **MAUVAIS**
```
Ce code est nul, ça ne marchera jamais.
Tu ne sais pas coder ou quoi ?
```

### 📝 Pour l'auteur de la PR

**Description de PR complète** :

```markdown
## 📋 Résumé
Ajout du système d'authentification avec Google OAuth

## 🎯 Contexte
Les utilisateurs demandent une connexion simplifiée (#123)

## 🔧 Changements
- Intégration du SDK Google OAuth 2.0
- Page de login avec bouton "Sign in with Google"
- Middleware d'authentification JWT
- Tests unitaires et d'intégration

## 🧪 Tests
- [x] Tests unitaires (95% coverage)
- [x] Tests d'intégration
- [x] Test manuel sur staging

## 📸 Screenshots
[image du bouton de login]

## ⚠️ Points d'attention
- Nécessite la variable d'env GOOGLE_CLIENT_ID
- Migration de base de données incluse

## 📚 Documentation
- README mis à jour
- Documentation API ajoutée

## 🔗 Liens
- Issue: #123
- Design: [Figma link]
- Documentation Google: https://...
```

---

## 5. Sécurité

### 🔐 Ce qu'il ne faut JAMAIS commiter

❌ **DANGER**
```javascript
// ❌ JAMAIS ça
const DB_PASSWORD = "motdepasse123";
const API_KEY = "sk_live_abc123def456";
const JWT_SECRET = "supersecret";
```

✅ **CORRECT**
```javascript
// ✅ Variables d'environnement
const DB_PASSWORD = process.env.DB_PASSWORD;
const API_KEY = process.env.API_KEY;
const JWT_SECRET = process.env.JWT_SECRET;
```

### 📄 .gitignore essentiel

```bash
# Secrets
.env
.env.local
.env.production
secrets.yaml
credentials.json

# Clés
*.pem
*.key
*.p12

# Fichiers système
.DS_Store
Thumbs.db

# Dependencies
node_modules/
vendor/
__pycache__/

# Build
dist/
build/
*.pyc
*.o

# IDE
.vscode/
.idea/
*.swp

# Logs
*.log
logs/

# Base de données locale
*.sqlite
*.db
```

### 🚨 Si vous avez commité des secrets

**ACTION IMMÉDIATE** :

```bash
# 1. Changer les credentials compromises MAINTENANT

# 2. Retirer du dernier commit (si pas pushé)
git rm --cached secrets.txt
git commit --amend

# 3. Retirer de l'historique (dangereux)
git filter-branch --tree-filter 'rm -f secrets.txt' HEAD
git push --force-with-lease

# 4. Ou utiliser BFG Repo Cleaner (recommandé)
bfg --delete-files secrets.txt
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

**PUIS** :
- Informer votre équipe
- Vérifier les logs d'accès
- Potentiellement contacter le support GitHub

---

## 6. Performance

### ⚡ Garder un repo léger

```bash
# Éviter de versionner
- Fichiers compilés (dist/, build/)
- Dependencies (node_modules/, vendor/)
- Fichiers volumineux (vidéos, gros datasets)
- Fichiers générés (coverage/, .next/)

# Pour les gros fichiers : Git LFS
git lfs install
git lfs track "*.psd"
git lfs track "*.mp4"
```

### 🗜️ Nettoyer l'historique

```bash
# Voir la taille du repo
git count-objects -vH

# Nettoyer
git gc --aggressive --prune=now

# Supprimer les branches locales obsolètes
git fetch --prune
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
```

### 📊 Analyser la taille

```bash
# Trouver les gros fichiers
git rev-list --objects --all \
  | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
  | sed -n 's/^blob //p' \
  | sort --numeric-sort --key=2 \
  | tail -n 10
```

---

## 7. Collaboration

### 👥 Communication d'équipe

**Avant de force push** :
```bash
# ⚠️ TOUJOURS prévenir l'équipe
# 1. Message sur Slack/Teams
"Je vais force push sur feature/xyz dans 5 min, 
pushez vos changements maintenant si vous travaillez dessus"

# 2. Attendre confirmation

# 3. Force push safer
git push --force-with-lease
# Refuse si quelqu'un a pushé entre temps
```

### 📢 Conventions d'équipe

Documenter dans `CONTRIBUTING.md` :

```markdown
# Contributing

## Workflow
1. Toujours partir de `develop` à jour
2. Nommage des branches : `type/description`
3. Commits selon convention Conventional Commits
4. PR obligatoire avec au moins 1 review
5. Squash avant merge si >5 commits

## Tests
- Tous les tests doivent passer
- Coverage minimum : 80%
- Tests E2E pour les features critiques

## Style
- ESLint + Prettier
- `npm run lint` avant commit
- Pre-commit hook configuré

## Review
- Maximum 48h pour review
- Commentaires constructifs
- Approuver uniquement si tests passent
```

---

## 8. Erreurs à Éviter

### ❌ Top 10 des erreurs

#### 1. Commiter directement sur main

```bash
# ❌ MAUVAIS
git checkout main
# ... modifications ...
git commit -m "fix stuff"

# ✅ BON
git checkout -b fix/critical-bug
# ... modifications ...
git commit -m "fix: correct critical bug"
# Créer une PR
```

#### 2. Force push sur branche partagée

```bash
# ❌ MAUVAIS
git push --force origin develop

# ✅ BON
git push --force-with-lease origin feature/ma-feature
# (et seulement sur VOS branches)
```

#### 3. Commits massifs

```bash
# ❌ MAUVAIS
git add .
git commit -m "update"
# 150 fichiers, 5000 lignes changées

# ✅ BON
# Plusieurs commits atomiques par fonctionnalité
```

#### 4. Messages inutiles

```bash
# ❌ MAUVAIS
git commit -m "fix"
git commit -m "update"
git commit -m "changes"

# ✅ BON
git commit -m "fix(auth): handle null user session"
```

#### 5. Ne pas pull avant push

```bash
# ❌ MAUVAIS
git push
# Rejeté car remote a changé

# ✅ BON
git pull --rebase
git push
```

#### 6. Rebase de commits publics

```bash
# ❌ MAUVAIS
git checkout develop  # Branche partagée
git rebase main
git push --force  # 💥 Chaos pour l'équipe

# ✅ BON
git checkout develop
git merge main
git push
```

#### 7. Ignorer les conflits

```bash
# ❌ MAUVAIS
# Résoudre vite fait et mal
git add .
git commit -m "fix conflicts"

# ✅ BON
# Prendre le temps de comprendre
# Tester après résolution
# Demander de l'aide si besoin
```

#### 8. Ne pas tester avant commit

```bash
# ❌ MAUVAIS
# ... modifications ...
git commit -m "feat: add new feature"
# Ça compile même pas 💥

# ✅ BON
npm test
npm run build
git commit -m "feat: add new feature"
```

#### 9. Branches qui vivent trop longtemps

```bash
# ❌ MAUVAIS
feature/mega-refactoring  # 3 mois de dev, 500 commits

# ✅ BON
feature/refactor-auth    # 1 semaine max
feature/refactor-api     # Découpage logique
```

#### 10. Ne pas synchroniser régulièrement

```bash
# ❌ MAUVAIS
# 2 semaines sans pull
git merge main
# 💥 200 conflits

# ✅ BON
# Tous les jours
git fetch origin
git rebase origin/main
```

---

## 🎯 Checklist Quotidienne

### Début de journée
- [ ] `git pull origin main`
- [ ] `git fetch --prune`
- [ ] Vérifier les nouvelles PR à review

### Pendant le développement
- [ ] Commits atomiques et fréquents
- [ ] Messages descriptifs
- [ ] Tests passent avant commit

### Fin de journée
- [ ] Push du travail en cours
- [ ] Synchroniser avec main si nécessaire
- [ ] Mettre à jour la PR si ouverte

### Avant une PR
- [ ] Rebase/merge avec main
- [ ] Tous les tests passent
- [ ] Lint passe
- [ ] Description complète de la PR
- [ ] Self-review du code

### Avant un merge
- [ ] Au moins 1 approbation
- [ ] CI/CD vert
- [ ] Pas de conflits
- [ ] Squash si nécessaire

---

**En suivant ces pratiques, vous éviterez 95% des problèmes Git ! 🎉**
