# Appli Android d'English Coach : guide

## Où on en est

L'appli fonctionne déjà comme une appli sur ton téléphone, sans rien installer depuis le Play Store :
dans Chrome sur Android, ouvre le site, puis choisis « Installer l'application » (ou « Ajouter à l'écran d'accueil »).
Les mises à jour du site arrivent toutes seules.

Une vraie appli Android (fichier .apk, ou publication sur le Play Store) demande une étape en plus. Ce guide la prépare.

## Deux méthodes possibles

| Méthode | Ce que c'est | Avantage | Limite |
|---|---|---|---|
| **TWA** (Trusted Web Activity), recommandée | Une petite appli Android qui ouvre le site dans le moteur Chrome | La reconnaissance vocale (micro) fonctionne comme dans Chrome | Il faut un fichier de vérification sur le domaine pour masquer la barre d'adresse |
| Capacitor (WebView) | Une appli qui affiche le site dans un navigateur intégré | Plus de contrôle natif | Le micro (reconnaissance vocale) n'est pas garanti dans ce navigateur intégré : à éviter pour English Coach |

Je recommande la **TWA**, parce que la prononciation vocale est au cœur de l'application.

## Ce qu'il faut sur ton ordinateur

- Node.js (version LTS) : https://nodejs.org
- Java JDK 17 : https://adoptium.net
- Android Studio (gratuit) : https://developer.android.com/studio
  Il installe le SDK Android. Lance-le une fois pour accepter les licences.

Le Play Store demande en plus un compte développeur Google, payant une seule fois (environ 25 USD). Ce coût est à prévoir avant une publication. Pour tester sur ton téléphone, un fichier .apk se fait sans frais.

## Étapes (TWA avec Bubblewrap)

1. Installe l'outil : `npm install -g @bubblewrap/cli`
2. Crée un dossier vide, par exemple `englishcoach-app`, et place-toi dedans.
3. Lance : `bubblewrap init --manifest https://rickifeeling-ux.github.io/english-coach/manifest.json`
   - Réponds aux questions (le nom de l'appli : English Coach ; l'identifiant : fr.englishcoach.app).
4. Construis l'appli : `bubblewrap build`. Il produit un fichier `app-release-signed.apk`, puis tu l'installes sur ton téléphone.

## Point à régler : la barre d'adresse

Sans un fichier de vérification, Chrome affiche une barre d'adresse au-dessus de l'appli.
Pour la retirer, il faut un fichier `assetlinks.json` à l'adresse
`https://rickifeeling-ux.github.io/.well-known/assetlinks.json`.
Cette adresse se trouve à la racine du site, donc dans un dépôt nommé `rickifeeling-ux.github.io`, et non dans `english-coach`.
Bubblewrap t'indique le contenu exact à mettre dans ce fichier.

## Ce qui n'est pas encore fait

- Le projet Android n'est pas généré : l'environnement où je travaille n'a pas accès aux gestionnaires de paquets (npm, pip) pour l'instant.
- Je ne peux pas non plus tester l'apk ici : il faut le SDK Android.
- Tu n'as pas besoin de faire tout cela tout de suite : l'installation depuis Chrome fonctionne déjà.
