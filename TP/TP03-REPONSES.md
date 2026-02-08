# TP03 - RÉPONSES

## 📋 Solution complète

### Étape 1 : Préparation du projet

```bash
# Créer le dossier et naviguer dedans
mkdir blog-project
cd blog-project

# Initialiser Git
git init

# Créer article.md
cat > article.md << 'EOF'
# Mon Premier Article

Ceci est mon premier article de blog.
EOF

# Ajouter et commiter
git add article.md
git commit -m "Initial article"
```

### Étape 2 : Création d'historique

```bash
# Modification 1 : Ajouter introduction
cat > article.md << 'EOF'
# Mon Premier Article

Ceci est mon premier article de blog.

## Introduction

Bienvenue sur mon blog de développement.
EOF

git add article.md
git commit -m "Add introduction section"

# Modification 2 : Ajouter motivation
cat >> article.md << 'EOF'

## Pourquoi ce blog?

Je veux partager mes connaissances en programmation.
EOF

git add article.md
git commit -m "Add motivation section"

# Modification 3 : Créer about.md
cat > about.md << 'EOF'
# À propos

Développeur passionné par JavaScript et Python.
EOF

git add about.md
git commit -m "Add about page"

# Modification 4 : Ajouter conclusion
cat >> article.md << 'EOF'

## Conclusion

Merci de votre lecture !
EOF

git add article.md
git commit -m "Add conclusion to article"
```

### Étape 3 : Explorer l'historique

```bash
# 13. Historique complet
git log
```

**Résultat** : Affiche tous les commits avec détails complets (hash, auteur, date, message)

```bash
# 14. Historique compact
git log --oneline
```

**Résultat** :
```
a1b2c3d Add conclusion to article
d4e5f6g Add about page
h7i8j9k Add motivation section
l0m1n2o Add introduction section
p3q4r5s Initial article
```

```bash
# 15. Historique avec statistiques
git log --stat
```

**Résultat** : Montre les fichiers modifiés et le nombre de lignes ajoutées/supprimées par commit

```bash
# 16. 3 derniers commits seulement
git log --oneline -3
# ou
git log --oneline -n 3
```

**Résultat** :
```
a1b2c3d Add conclusion to article
d4e5f6g Add about page
h7i8j9k Add motivation section
```

```bash
# 17. Historique d'un fichier spécifique
git log article.md
# ou avec --oneline
git log --oneline article.md
```

**Résultat** : Seulement les commits qui ont modifié `article.md`
```
a1b2c3d Add conclusion to article
h7i8j9k Add motivation section
l0m1n2o Add introduction section
p3q4r5s Initial article
```

### Étape 4 : Comparer des versions

```bash
# 18. Comparer HEAD avec HEAD~1 (commit actuel vs précédent)
git diff HEAD~1 HEAD
# ou simplement
git diff HEAD~1
```

**Résultat** : Montre ce qui a été ajouté dans le dernier commit (section Conclusion)

```bash
# 19. Comparer premier et dernier commit
git log --oneline  # pour voir les IDs
git diff p3q4r5s a1b2c3d
# ou avec des références relatives
git diff HEAD~4 HEAD
```

**Résultat** : Montre TOUTES les différences entre la version initiale et la version finale

```bash
# 20. Différences dans article.md entre 2ème et 4ème commit
git log --oneline  # identifier les commits
git diff l0m1n2o d4e5f6g article.md
# ou
git diff HEAD~3 HEAD~1 article.md
```

**Résultat** : Montre l'ajout de la section "Pourquoi ce blog?"

### Étape 5 : Voyager dans le temps

```bash
# 21. Noter l'ID du commit "Add introduction section"
git log --oneline
# Supposons que c'est l0m1n2o

# 22. Checkout vers ce commit
git checkout l0m1n2o
```

**Résultat** :
```
Note: switching to 'l0m1n2o'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

HEAD is now at l0m1n2o Add introduction section
```

```bash
# 23. Vérifier le contenu de article.md
cat article.md
```

**Résultat** :
```markdown
# Mon Premier Article

Ceci est mon premier article de blog.

## Introduction

Bienvenue sur mon blog de développement.
```

**Note** : Les sections "Pourquoi ce blog?" et "Conclusion" n'existent pas encore à ce stade !

```bash
# 24. Vérifier si about.md existe
ls -la
cat about.md  # Erreur : fichier n'existe pas
```

**Résultat** : `about.md` n'existe PAS car il a été créé après ce commit.

```bash
# 25. Afficher le log
git log --oneline
```

**Résultat** : Vous ne voyez QUE les commits jusqu'à ce point :
```
l0m1n2o Add introduction section
p3q4r5s Initial article
```

Les commits futurs (motivation, about, conclusion) sont "cachés" car ils n'existent pas encore dans cette timeline.

### Étape 6 : Retour au présent

```bash
# 26. Retour sur main
git checkout main
# ou
git switch main
```

**Résultat** :
```
Previous HEAD position was l0m1n2o Add introduction section
Switched to branch 'main'
```

```bash
# 27. Vérifier les fichiers
ls -la
cat article.md
cat about.md
```

**Résultat** : Tous les fichiers et leur contenu complet sont revenus !

```bash
# 28. Vérifier l'historique complet
git log --oneline
```

**Résultat** : Tous les 5 commits sont de nouveau visibles !

### Étape 7 : Examiner un commit spécifique

```bash
# 29. Détails du commit "Add about page"
git log --oneline  # trouver l'ID : d4e5f6g
git show d4e5f6g
```

**Résultat** : Affiche :
- Les métadonnées du commit (auteur, date)
- Le message
- Les différences (diff) introduites par ce commit

```bash
# 30. Seulement les fichiers modifiés
git show d4e5f6g --name-only
```

**Résultat** :
```
commit d4e5f6g...
Author: ...
Date: ...

    Add about page

about.md
```

```bash
# 31. Contenu d'un fichier à un commit sans checkout
git show l0m1n2o:article.md
```

**Résultat** : Affiche le contenu de `article.md` tel qu'il était au commit "Add introduction section"

### Étape 8 : Historique visuel

```bash
# 32. Graphe de l'historique
git log --graph --oneline --all
```

**Résultat** (pour un historique linéaire) :
```
* a1b2c3d Add conclusion to article
* d4e5f6g Add about page
* h7i8j9k Add motivation section
* l0m1n2o Add introduction section
* p3q4r5s Initial article
```

```bash
# 33. Format personnalisé avec date et auteur
git log --pretty=format:"%h - %an, %ar : %s" --graph
```

**Résultat** :
```
* a1b2c3d - John Doe, 2 hours ago : Add conclusion to article
* d4e5f6g - John Doe, 3 hours ago : Add about page
* h7i8j9k - John Doe, 5 hours ago : Add motivation section
* l0m1n2o - John Doe, 6 hours ago : Add introduction section
* p3q4r5s - John Doe, 7 hours ago : Initial article
```

**Autre format utile** :
```bash
git log --pretty=format:"%C(yellow)%h%C(reset) - %C(cyan)%an%C(reset), %C(green)%ar%C(reset) : %s" --graph
```

## ✅ Réponses aux validations

### Combien de commits au total ?

```bash
git log --oneline | wc -l
# ou
git rev-list --count HEAD
```

**Résultat** : `5`

### Quel est le message du 3ème commit ?

```bash
git log --oneline | head -3 | tail -1
# ou
git log --oneline --reverse | head -3 | tail -1
```

**Résultat** : `Add motivation section` (en comptant depuis le plus récent)

### Combien de lignes ajoutées au total dans article.md ?

```bash
git log --oneline article.md --numstat
# ou mieux
git log --oneline article.md -- | head -1 | xargs git diff --stat p3q4r5s
```

Alternative plus simple :
```bash
git diff p3q4r5s HEAD -- article.md --stat
```

### Quelle était la version de article.md il y a 3 commits ?

```bash
git show HEAD~3:article.md
```

## 🎓 Réponses aux questions de réflexion

### 1. Qu'est-ce qu'un "detached HEAD" ?

**Détached HEAD** = HEAD pointe directement sur un commit plutôt que sur une branche.

**Normalement** :
```
HEAD → main → commit123
```

**En detached HEAD** :
```
HEAD → commit123
```

**Pourquoi Git avertit ?**
- Les commits faits dans cet état ne sont attachés à aucune branche
- Si vous changez de branche, ces commits seront "perdus" (orphelins)
- Ils resteront 30 jours dans le reflog puis seront garbage collected

**Quand l'utiliser ?**
- Pour inspecter un ancien état
- Pour tester quelque chose temporairement
- Pour créer une branche depuis cet état : `git checkout -b nouvelle-branche`

**Comment en sortir ?**
- `git checkout main` (ou n'importe quelle branche)
- `git switch main`

### 2. Différence entre `git log` et `git show` ?

| Commande | Fonction | Utilisation |
|----------|----------|-------------|
| `git log` | Liste PLUSIEURS commits | Voir l'historique |
| `git show` | Détails d'UN SEUL commit | Examiner un commit précis |

**git log** :
```bash
git log              # tous les commits
git log --oneline    # format compact
git log -5           # 5 derniers
git log fichier.js   # commits touchant ce fichier
```

**git show** :
```bash
git show abc123      # détails + diff du commit abc123
git show HEAD        # dernier commit
git show HEAD~2      # il y a 2 commits
git show abc123:file.js  # contenu de file.js à ce commit
```

**Analogie** :
- `git log` = table des matières d'un livre
- `git show` = lire une page spécifique

### 3. Comment trouver quand une ligne spécifique a été ajoutée ?

**Méthode 1 : git blame**
```bash
git blame article.md
```

**Résultat** :
```
p3q4r5s (John Doe 2024-01-01) # Mon Premier Article
p3q4r5s (John Doe 2024-01-01) 
l0m1n2o (John Doe 2024-01-01) ## Introduction
l0m1n2o (John Doe 2024-01-01) Bienvenue sur mon blog
```

Chaque ligne montre : commit-id, auteur, date, puis le contenu.

**Méthode 2 : git log -S (pickaxe)**
```bash
git log -S "Introduction" --oneline
```

Trouve les commits qui ont ajouté ou supprimé le mot "Introduction".

**Méthode 3 : git log -G (regex)**
```bash
git log -G "^## Introduction" --oneline
```

Plus puissant, permet des regex.

**Méthode 4 : git log -L (range)**
```bash
git log -L 5,8:article.md
```

Historique des lignes 5 à 8 spécifiquement.

### 4. Pourquoi checkout sur un commit plutôt que créer une branche ?

**Utiliser `git checkout <commit>` (detached HEAD) quand** :
- ✅ Inspection rapide d'un ancien état
- ✅ Test temporaire sans laisser de trace
- ✅ Vérification d'un bug à une version précise
- ✅ Démo d'une ancienne fonctionnalité

**Créer une branche quand** :
- ✅ Vous voulez faire des modifications
- ✅ Vous voulez garder cet état pour plus tard
- ✅ Vous voulez développer depuis ce point
- ✅ Vous voulez merger ces changements

**Exemple de workflow** :
```bash
# Inspection rapide
git checkout abc123
cat fichier.js  # juste pour voir
git checkout main  # retour

# Si vous voulez modifier
git checkout abc123
git checkout -b fix-depuis-ancienne-version
# maintenant vous pouvez commiter
```

## 🧪 Réponses aux défis

### Trouver le commit qui a introduit "Python"

```bash
git log -S "Python" --oneline
# ou
git log --all --grep="Python"
# ou
git log -G "Python" --oneline
```

**Résultat** : `d4e5f6g Add about page`

### Commits ayant modifié article.md

```bash
git log --oneline article.md
```

### Créer un alias pour votre format préféré

```bash
git config --global alias.lg "log --graph --pretty=format:'%C(yellow)%h%C(reset) - %C(cyan)%an%C(reset), %C(green)%ar%C(reset) : %s' --abbrev-commit"

# Utilisation
git lg
```

### Utiliser git blame

```bash
git blame article.md
```

**Sortie** :
```
p3q4r5s 1 # Mon Premier Article
p3q4r5s 2 
p3q4r5s 3 Ceci est mon premier article de blog.
p3q4r5s 4 
l0m1n2o 5 ## Introduction
l0m1n2o 6 
l0m1n2o 7 Bienvenue sur mon blog de développement.
h7i8j9k 8 
h7i8j9k 9 ## Pourquoi ce blog?
```

**Pour voir la date aussi** :
```bash
git blame -L 1,10 --date=short article.md
```

## 💡 Points clés à retenir

1. **HEAD** = pointeur vers votre commit actuel
2. **HEAD~1** = commit parent (1 commit en arrière)
3. **HEAD~3** = 3 commits en arrière
4. **Detached HEAD** = inspection temporaire, pas pour commiter
5. **git show** = pour UN commit, **git log** = pour PLUSIEURS
6. **git blame** = qui a écrit quoi et quand
7. **Toujours revenir sur une branche** après inspection

## 🚀 Commandes bonus avancées

### Voir l'historique de façon interactive

```bash
git log --graph --all --decorate --oneline --color
```

### Chercher un commit par message

```bash
git log --grep="bug" --oneline
```

### Voir qui a fait le plus de commits

```bash
git shortlog -sn
```

### Statistiques par auteur

```bash
git log --author="John" --stat
```

---

**Bravo ! Vous savez maintenant naviguer dans l'historique Git comme un pro ! 🎉**

Passez au TP04 pour maîtriser les branches.
