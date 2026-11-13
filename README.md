# Suivi Top 3 équipe : mise en ligne

Site web du suivi d'équipe (PE Batilly - PE Logistique) : présence, Top 3 de la semaine avec jours prévus, priorité du jour, actions en attente, relances.
Aucun compte pour les collègues : ils ouvrent le lien de l'équipe, sur PC ou téléphone.

- **Données** : Firebase Firestore (base en ligne de Google, offre gratuite « Spark »).
- **Site** : GitHub Pages (hébergement gratuit).
- **Fichiers** : `index.html` (le site), `firestore.rules` (règles d'accès), ce `README.md`.

Compter 15 minutes, une seule fois.

---

## 1. Firebase (la base de données)

1. Va sur <https://console.firebase.google.com> > **Ajouter un projet**. Nom : `suivi-top3`. Google Analytics : **non**.
2. **Authentication** > **Commencer** > onglet **Méthode de connexion** > **Anonyme** > **Activer** > Enregistrer.
3. **Firestore Database** > **Créer une base de données**.
   - Emplacement : **europe-west9 (Paris)**, ou `eur3 (Europe)`. Ce choix est définitif.
   - Mode : **production**.
4. Firestore > onglet **Règles** : remplace tout par le contenu de `firestore.rules`, puis **Publier**.
5. ⚙ **Paramètres du projet** > **Vos applications** > icône **Web `</>`**.
   - Nom : `suivi-top3-web`. Ne coche pas « Hosting ».
   - Firebase affiche un bloc `firebaseConfig`. Copie ces 4 valeurs dans `index.html`, en haut du script :

```js
const FIREBASE_CONFIG = {
  apiKey: "AIza…",
  authDomain: "suivi-top3-xxxx.firebaseapp.com",
  projectId: "suivi-top3-xxxx",
  appId: "1:…:web:…",
};
```

Ces valeurs ne sont pas secrètes : la protection vient des règles et du lien d'équipe.

## 2. GitHub Pages (le site)

1. Sur <https://github.com> > **New repository**. Nom : `suivi-top3`, visibilité **Public** (obligatoire pour Pages gratuit).
2. **Add file** > **Upload files** : dépose `index.html` (avec la configuration), `firestore.rules` et `README.md` > **Commit changes**.
3. **Settings** > **Pages** > Source : **Deploy from a branch**, branche **main**, dossier **/ (root)** > **Save**.
4. Une minute plus tard, le site est en ligne : `https://TON-PSEUDO.github.io/suivi-top3/`
5. Dans Firebase > **Authentication** > **Paramètres** > **Domaines autorisés** : ajoute `TON-PSEUDO.github.io`.

## 3. Créer l'équipe

1. Ouvre le site > écris ton nom > **Créer l'équipe** (ex. « PE Logistique · AMR »).
2. **Copier le lien**, puis envoie-le dans le canal Teams de l'équipe.
   - Le lien finit par `#t=` suivi de 24 caractères : c'est la clé de l'équipe.
3. ⚙ > **Gérer l'équipe** : ajoute les personnes, avec leur e-mail pour les relances Teams.

Les collègues ouvrent le lien, choisissent leur nom, et c'est tout. Pour un raccourci : favori du navigateur, ou « Ajouter à l'écran d'accueil » sur téléphone.

## 4. Reprendre les données de la version « dossier Teams » (facultatif)

1. Dans l'ancien fichier `Suivi_Top3_equipe.html` : ⚙ > Sauvegarde > **Enregistrer**. Un fichier `.json` est créé.
2. Dans le site, équipe ouverte : ⚙ > Sauvegarde > **Ouvrir / restaurer** > choisis ce fichier.

Rien n'est écrasé par une donnée plus ancienne.

## 5. Points d'attention

- **Données hors du SI de l'entreprise.** Les noms, objectifs, présences et absences sont stockés chez Google, sur ton compte personnel. Fais valider par ton responsable ou l'informatique (RGPD) avant de l'ouvrir à l'équipe. Pour limiter : base en Europe, prénoms seulement, e-mails facultatifs.
- **Réseau de l'usine.** Teste depuis un PC du site : il doit joindre `github.io`, `gstatic.com` et `firestore.googleapis.com`. Sinon, le bandeau rouge « Connexion à la base impossible » s'affiche.
- **Le code est public, pas les données.** Sans le lien d'équipe, personne ne peut lire ni écrire, et les équipes ne peuvent pas être listées. Si le lien circule trop : ⚙ > Sauvegarde > Enregistrer, crée une nouvelle équipe, restaure la sauvegarde, puis envoie le nouveau lien.
- **Quotas gratuits Firebase.** 50 000 lectures et 20 000 écritures par jour, largement assez pour une équipe. Le site ne lit que la semaine affichée.
- **Hors ligne.** On peut continuer à saisir ; l'envoi se fait au retour du réseau.

## Mettre à jour le site

Sur GitHub, ouvre `index.html` > crayon **Edit**, ou **Add file** > **Upload files** avec la nouvelle version. Garde le bloc `FIREBASE_CONFIG`.
Les données ne bougent pas : elles sont dans Firebase.
