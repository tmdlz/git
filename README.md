# Guide d'installation Git sur Windows

## 📥 1. Téléchargement

Rendez-vous sur le site officiel de Git :
**[https://git-scm.com/download/windows](https://git-scm.com)**

Le téléchargement démarre automatiquement. Sinon, cliquez sur le bouton de téléchargement.

---

## ⚙️ 2. Installation

1. **Lancez l'installateur** `.exe` téléchargé
2. **Gardez les options par défaut** en cliquant sur "Next"
3. **Options importantes à vérifier** :
   - ✅ "Git Bash Here" (menu contextuel)
   - ✅ "Git from the command line and also from 3rd-party software"
   - ✅ "Use bundled OpenSSH"

4. Terminez l'installation

---

## ✔️ 3. Vérification de l'installation

Ouvrez **PowerShell**, **CMD** ou **Git Bash** et tapez :

```bash
git --version
```

**Résultat attendu** :
```
git version 2.43.0.windows.1
```

✅ Si vous voyez un numéro de version, Git est installé correctement !

---

## 🔧 4. Configuration initiale

### Identité Git (obligatoire)

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre-email@example.com"
```

⚠️ **Important** : Utilisez le même email que votre compte GitHub

### Vérifier la configuration

```bash
git config --list
```

---

## 🔐 5. Configuration SSH pour GitHub

### Étape 1 : Générer une clé SSH

Ouvrez **Git Bash** et exécutez :

```bash
ssh-keygen -t ed25519 -C "votre-email@example.com"
```

**Appuyez sur Entrée** trois fois pour accepter :
- L'emplacement par défaut (`~/.ssh/id_ed25519`)
- Pas de passphrase (ou entrez-en une si vous voulez plus de sécurité)

**Résultat** :
```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/VotreNom/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/VotreNom/.ssh/id_ed25519
Your public key has been saved in /c/Users/VotreNom/.ssh/id_ed25519.pub
```

---

### Étape 2 : Copier la clé publique

```bash
cat ~/.ssh/id_ed25519.pub
```

**Copiez tout le texte** qui s'affiche (commence par `ssh-ed25519` et finit par votre email)

Ou utilisez cette commande pour copier directement dans le presse-papiers :

```bash
clip < ~/.ssh/id_ed25519.pub
```

---

### Étape 3 : Ajouter la clé sur GitHub

1. **Connectez-vous à GitHub** : [https://github.com](https://github.com)

2. **Cliquez sur votre avatar** (en haut à droite) → **Settings**

3. Dans le menu de gauche : **SSH and GPG keys**

4. Cliquez sur **"New SSH key"**

5. **Remplissez le formulaire** :
   - **Title** : `Mon PC Windows` (ou un nom identifiant votre machine)
   - **Key type** : `Authentication Key`
   - **Key** : Collez la clé copiée précédemment

6. Cliquez sur **"Add SSH key"**

7. **Confirmez avec votre mot de passe** GitHub si demandé

---

### Étape 4 : Tester la connexion SSH

Dans **Git Bash**, tapez :

```bash
ssh -T git@github.com
```

**Première fois** : Tapez `yes` pour accepter l'empreinte de GitHub

**Résultat attendu** :
```
Hi VotreNom! You've successfully authenticated, but GitHub does not provide shell access.
```

✅ **C'est bon !** Votre SSH est configuré correctement.

---

## 🚀 6. Utilisation avec GitHub

### Cloner un repo en SSH

```bash
git clone git@github.com:username/repo.git
```

### Commandes de base

```bash
# Ajouter des fichiers
git add .

# Créer un commit
git commit -m "Description du commit"

# Envoyer sur GitHub
git push
```

---

## 📝 Notes importantes

- **HTTPS vs SSH** : Avec SSH, vous n'aurez plus besoin d'entrer vos identifiants à chaque push
- **Token vs SSH** : SSH est plus pratique pour un usage quotidien
- **Plusieurs machines** : Répétez les étapes 5.1 à 5.3 pour chaque ordinateur (avec un titre différent)

---

## 🔗 Ressources utiles

- Documentation Git : [https://git-scm.com/doc](https://git-scm.com/doc)
- GitHub SSH Docs : [https://docs.github.com/en/authentication/connecting-to-github-with-ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- GitHub CLI (alternative) : [https://cli.github.com](https://cli.github.com)

---

**Fait avec ❤️ pour une installation simple et efficace**
