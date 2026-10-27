# Carnet de notes

Site de suivi des notes et bulletins (professeurs, administrateur, parents).
Front : un seul fichier `index.html` hébergé sur **GitHub Pages**.
Base de données : **Firebase Firestore** (gratuit pour un usage scolaire normal).

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète |
| `config.js` | Vos 4 clés Firebase |
| `firestore.rules` | Règles de sécurité de la base (à coller dans Firebase) |
| `.nojekyll` | Demande à GitHub Pages de servir les fichiers tels quels |

## 1. Créer la base de données (Firebase)

1. Sur https://console.firebase.google.com, créez un projet.
2. **Authentication** > Méthode de connexion : activez **E-mail/Mot de passe**.
3. **Firestore Database** : créez la base en **mode production**.
4. Onglet **Règles** : remplacez tout par le contenu de `firestore.rules`, puis **Publier**.
5. **Paramètres du projet** > **Vos applications** > ajoutez une application **Web**, puis copiez `apiKey`, `authDomain`, `projectId`, `appId` dans `config.js`.
6. **Authentication** > **Paramètres** > **Domaines autorisés** : ajoutez `VOTRE-PSEUDO.github.io`.

## 2. Publier sur GitHub Pages

1. Créez un dépôt GitHub (public, ou privé avec un compte qui autorise Pages).
2. Envoyez-y les 4 fichiers de ce dossier (bouton **Add file > Upload files**).
3. **Settings** > **Pages** > Source : **Deploy from a branch**, branche `main`, dossier `/ (root)` > **Save**.
4. Après 1 à 2 minutes, le site est en ligne sur `https://VOTRE-PSEUDO.github.io/NOM-DU-DEPOT/`.

## 3. Créer le code administrateur

Dans Firestore, créez la collection `invitations` avec un document dont **l'identifiant est votre code** (10 caractères MAJUSCULES et chiffres minimum, ex. `K7M2QX4R9B`) et deux champs :

- `nom` (texte) : `Direction`
- `admin` (booléen) : `true`

Ensuite, tout se fait dans l'application : l'administrateur ouvre l'espace professeurs, saisit son code, puis crée un code personnel pour chaque professeur. Les parents consultent le bulletin avec le code de leur enfant, sans compte.

## Sécurité

- Les clés de `config.js` sont publiques par conception ; la protection vient des règles Firestore.
- Gardez confidentiels le code administrateur et les codes professeurs.
- Ne publiez jamais de données réelles d'élèves avant d'avoir publié les règles.
