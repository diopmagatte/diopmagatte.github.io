# 🛡️ Guide de déploiement — Portfolio Security Analyst
## Hugo + Thème Toha → GitHub Pages

---

## 📋 Prérequis

Assure-toi d'avoir installé sur ta machine :

| Outil | Version minimale | Lien |
|-------|-----------------|------|
| Git | 2.x | https://git-scm.com |
| Hugo **Extended** | 0.110+ | https://gohugo.io/installation/ |
| Go | 1.21+ | https://go.dev/dl/ |
| Node.js | 18+ | https://nodejs.org |

> ⚠️ **Important** : Hugo doit être la version **Extended** (nécessaire pour le thème Toha qui utilise SCSS).
> Vérifie avec : `hugo version` → tu dois voir `extended` dans la sortie.

---

## 🚀 Étape 1 — Cloner ton repo GitHub Pages

```bash
# Remplace "johndoe" par ton vrai username GitHub
git clone https://github.com/johndoe/johndoe.github.io.git
cd johndoe.github.io
```

---

## 📂 Étape 2 — Copier les fichiers du portfolio

Copie **tous les fichiers fournis** dans ton repo cloné en respectant la structure suivante :

```
johndoe.github.io/
├── .github/
│   └── workflows/
│       └── deploy.yml          ✅ workflow GitHub Actions
├── config/
│   └── _default/
│       ├── config.yaml         ✅ configuration principale Hugo
│       └── module.yaml         ✅ import du thème Toha
├── content/
│   ├── en/
│   │   └── _index.md           ✅ page d'accueil (anglais)
│   └── fr/
│       └── _index.md           ✅ page d'accueil (français)
├── data/
│   ├── en/
│   │   ├── about.yaml          ✅ infos personnelles
│   │   ├── experiences.yaml    ✅ expériences
│   │   ├── projects.yaml       ✅ projets
│   │   ├── skills.yaml         ✅ compétences
│   │   ├── certifications.yaml ✅ certifications
│   │   └── contact.yaml        ✅ contact
│   └── fr/
│       ├── about.yaml
│       ├── experiences.yaml
│       ├── projects.yaml
│       ├── skills.yaml
│       ├── certifications.yaml
│       └── contact.yaml
├── static/
│   └── images/                 ← tes images (voir Étape 4)
├── go.mod                      ✅ module Go pour Hugo
└── .gitignore                  ✅
```

---

## 📦 Étape 3 — Installer le thème Toha et les dépendances

```bash
# Dans le dossier de ton repo
cd johndoe.github.io

# Télécharger le thème via Hugo Modules
hugo mod get github.com/hugo-toha/toha/v4

# Installer les dépendances Node.js du thème
hugo mod npm pack
npm install
```

---

## 🖼️ Étape 4 — Ajouter tes images

Place tes images dans `static/images/` selon cette structure :

```
static/images/
├── background.jpg              ← image de fond de la page d'accueil (1920x1080 recommandé)
├── main-logo.png               ← logo principal (sidebar)
├── inverted-logo.png           ← logo inversé (navbar)
├── favicon.png                 ← favicon (32x32)
├── author/
│   └── john-doe.jpg            ← ta photo de profil
├── sections/
│   ├── skills/
│   │   ├── security.png
│   │   ├── network.png
│   │   ├── threat.png
│   │   ├── vuln.png
│   │   ├── code.png
│   │   └── cloud.png
│   ├── experiences/
│   │   ├── cybershield.png
│   │   ├── securenet.png
│   │   └── infosec.png
│   └── projects/
│       ├── siem.png
│       ├── threat-intel.png
│       ├── phishing.png
│       ├── homelab.png
│       ├── playbooks.png
│       └── cve.png
```

> 💡 **Astuce** : Pour commencer rapidement, tu peux utiliser des logos simples
> depuis https://simpleicons.org ou même des emojis en PNG.
> Toha affiche un logo générique si l'image est manquante — le site fonctionnera quand même.

---

## ✏️ Étape 5 — Personnaliser ton contenu

Ouvre les fichiers YAML et remplace les valeurs exemples par tes vraies informations :

### `config/_default/config.yaml`
```yaml
baseURL: https://TON-USERNAME.github.io   # ← ton vrai username
title: "Ton Nom | Security Analyst"
gitRepo: https://github.com/TON-USERNAME/TON-USERNAME.github.io
```

### `data/en/about.yaml` et `data/fr/about.yaml`
- Remplace `John Doe` par ton nom
- Mets à jour le résumé, l'email, le téléphone, les liens sociaux

### `data/en/experiences.yaml` et `data/fr/experiences.yaml`
- Remplace les entreprises et postes par ton vrai parcours

### `data/en/certifications.yaml` et `data/fr/certifications.yaml`
- Garde seulement les certifications que tu possèdes réellement

---

## 🔍 Étape 6 — Tester localement

```bash
# Lancer le serveur de développement Hugo
hugo server -D

# Ouvre dans ton navigateur :
# http://localhost:1313
```

> Si tu vois une erreur de module, relance :
> ```bash
> hugo mod tidy
> npm install
> ```

---

## ⚙️ Étape 7 — Configurer GitHub Pages

1. Va sur **github.com/TON-USERNAME/TON-USERNAME.github.io**
2. Clique sur **Settings** → **Pages**
3. Dans **Source**, sélectionne **GitHub Actions**
4. C'est tout ! Le workflow `deploy.yml` s'occupera du reste.

---

## 📤 Étape 8 — Publier ton portfolio

```bash
# Ajouter tous les fichiers
git add .

# Commit initial
git commit -m "feat: initial portfolio setup with Hugo Toha theme"

# Pousser sur GitHub
git push origin main
```

Le workflow GitHub Actions se déclenche automatiquement.
Dans **2-3 minutes**, ton site sera live sur :

```
https://johndoe.github.io
```

Tu peux suivre le déploiement dans **Actions** → **Deploy Portfolio to GitHub Pages**.

---

## 🔄 Mise à jour du site

À chaque fois que tu veux modifier ton portfolio :

```bash
# Modifie les fichiers YAML dans data/en/ ou data/fr/
# Puis :
git add .
git commit -m "update: ajout nouveau projet / certification / etc."
git push origin main
```

Le site se redéploie automatiquement en ~2 minutes. ✅

---

## 🛠️ Commandes utiles

| Commande | Description |
|----------|-------------|
| `hugo server -D` | Serveur local avec hot-reload |
| `hugo build --minify` | Générer le site en production |
| `hugo mod get -u` | Mettre à jour le thème Toha |
| `hugo mod tidy` | Nettoyer les dépendances Go |
| `npm install` | Réinstaller les dépendances Node |

---

## ❓ Problèmes courants

### ❌ "module not found" au lancement
```bash
hugo mod get github.com/hugo-toha/toha/v4
hugo mod tidy
npm install
```

### ❌ "hugo: command not found"
Installe Hugo Extended : https://gohugo.io/installation/

### ❌ Le site s'affiche mais sans style (CSS cassé)
Vérifie que `baseURL` dans `config.yaml` correspond exactement à ton URL GitHub Pages.

### ❌ Le workflow GitHub Actions échoue
- Vérifie que **Settings → Pages → Source** est bien sur **GitHub Actions**
- Vérifie que le repo est **public** (GitHub Pages gratuit = repo public)

---

## 📚 Ressources utiles

- 📖 Documentation Toha : https://toha-guides.netlify.app/posts/
- 🎨 Démo live Toha : https://hugo-toha.github.io
- 📦 Hugo Modules : https://gohugo.io/hugo-modules/
- 🔧 GitHub Actions Pages : https://github.com/actions/deploy-pages

---

*Bonne chance avec ton portfolio ! 🛡️*
