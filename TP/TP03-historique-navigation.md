# TP03 - Navigation dans l'Historique

## 🎯 Objectifs

- Utiliser `git log` avec différentes options
- Naviguer entre les commits avec `git checkout`
- Comprendre le concept de HEAD détaché
- Comparer des commits avec `git diff`
- Examiner l'historique d'un fichier spécifique

## 📝 Contexte

Vous reprenez un projet existant et devez comprendre son évolution. Vous allez apprendre à explorer l'historique, à voir les changements entre versions, et à revenir temporairement à d'anciennes versions pour inspection.

## 🔧 Instructions

### Étape 1 : Préparation du projet

1. Créez un nouveau dossier `blog-project`
2. Initialisez Git
3. Créez un fichier `article.md` avec ce contenu :

```markdown
# Mon Premier Article

Ceci est mon premier article de blog.
```

4. Commitez avec "Initial article"

### Étape 2 : Création d'historique

5. Modifiez `article.md` pour ajouter une section :

```markdown
# Mon Premier Article

Ceci est mon premier article de blog.

## Introduction

Bienvenue sur mon blog de développement.
```

6. Commitez avec "Add introduction section"

7. Ajoutez encore du contenu :

```markdown
## Pourquoi ce blog?

Je veux partager mes connaissances en programmation.
```

8. Commitez avec "Add motivation section"

9. Créez un nouveau fichier `about.md` :

```markdown
# À propos

Développeur passionné par JavaScript et Python.
```

10. Commitez avec "Add about page"

11. Modifiez `article.md` en ajoutant :

```markdown
## Conclusion

Merci de votre lecture !
```

12. Commitez avec "Add conclusion to article"

### Étape 3 : Explorer l'historique

13. Affichez l'historique complet avec toutes les informations
14. Affichez l'historique en format compact (une ligne par commit)
15. Affichez l'historique avec les statistiques de modifications
16. Affichez uniquement les 3 derniers commits
17. Affichez l'historique du fichier `article.md` uniquement

### Étape 4 : Comparer des versions

18. Comparez le commit actuel avec l'avant-dernier commit
19. Comparez le premier commit avec le dernier
20. Affichez les différences dans le fichier `article.md` entre le 2ème et 4ème commit

### Étape 5 : Voyager dans le temps

21. Notez l'ID du commit "Add introduction section"
22. Utilisez `git checkout` pour revenir à ce commit
23. Vérifiez le contenu de `article.md` - que contient-il ?
24. Vérifiez si le fichier `about.md` existe
25. Affichez le log - combien de commits voyez-vous ?

### Étape 6 : Retour au présent

26. Retournez sur la branche principale (main/master)
27. Vérifiez que tous les fichiers sont revenus
28. Vérifiez que l'historique complet est de nouveau visible

### Étape 7 : Examiner un commit spécifique

29. Affichez les détails complets du commit "Add about page"
30. Affichez uniquement les fichiers modifiés dans ce commit
31. Affichez le contenu d'un fichier à un commit spécifique (sans checkout)

### Étape 8 : Historique visuel

32. Affichez un graphe de l'historique (même s'il est linéaire pour l'instant)
33. Utilisez une commande personnalisée pour un affichage formaté avec date et auteur

## ✅ Validation

Répondez à ces questions en utilisant UNIQUEMENT des commandes Git :

```bash
# Combien de commits au total ?
# Commande : _______________

# Quel est le message du 3ème commit ?
# Commande : _______________

# Combien de lignes ont été ajoutées au total dans article.md ?
# Commande : _______________

# Quelle était la version de article.md il y a 3 commits ?
# Commande : _______________
```

## 🎓 Questions de réflexion

1. Qu'est-ce qu'un "detached HEAD" et pourquoi Git vous avertit ?
2. Quelle est la différence entre `git log` et `git show` ?
3. Comment retrouver quand une ligne spécifique a été ajoutée ?
4. Pourquoi utiliser `git checkout` sur un commit plutôt que créer une branche ?

## 🧪 Défis supplémentaires

- Trouvez le commit qui a introduit le mot "Python"
- Affichez uniquement les commits qui ont modifié `article.md`
- Créez un alias Git pour votre format de log préféré
- Utilisez `git blame` sur `article.md`

---

⚠️ **Ne consultez les réponses qu'après avoir essayé !**

Réponses disponibles dans : `TP03-REPONSES.md`
