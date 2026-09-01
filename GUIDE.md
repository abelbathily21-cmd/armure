# Armure — installer l'appli sur vos deux iPhone

Coût : 0 €. Aucune carte bancaire n'est demandée nulle part.
Le plus confortable est de faire les étapes 1 à 3 sur un ordinateur, mais tout est faisable depuis l'iPhone.

Fichiers de ce dossier (à ne pas renommer) : `index.html`, `app.js`, `manifest.json`, `sw.js`, `icon-180.png`, `icon-192.png`, `icon-512.png`, `favicon.png`.
Le fichier `firestore.rules` sert à l'étape 2. Ce guide n'a pas besoin d'être mis en ligne.

---

## 1. Créer la base de données (Firebase, gratuit)

1. Va sur https://console.firebase.google.com et connecte-toi avec un compte Google (le tien ou celui de ta mère).
2. « Créer un projet » → nom : `armure` → tu peux désactiver Google Analytics → « Créer le projet ».
3. Menu de gauche : **Créer** → **Firestore Database** → « Créer une base de données ».
   - Emplacement : `europe-west` (n'importe lequel en Europe).
   - Mode : choisis **« Démarrer en mode test »** puis « Activer ».

## 2. Mettre les règles de sécurité définitives

Le mode test s'éteint tout seul au bout de 30 jours ; on met des règles permanentes tout de suite.

1. Dans Firestore Database, onglet **Règles**.
2. Efface tout et colle exactement ceci (c'est aussi le contenu du fichier `firestore.rules`) :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /armure/{docId} {
      allow get, create, update: if true;
      allow list, delete: if false;
    }
  }
}
```

3. « Publier ».

Ce que ça fait : seule une personne qui connaît votre code famille peut lire ou modifier vos données ; personne ne peut lister ni supprimer.

## 3. Configuration Firebase

Déjà faite : la configuration du projet `armure-2d4fd` est intégrée dans l'appli. Rien à copier.

## 4. Mettre l'appli en ligne (GitHub Pages, gratuit)

1. Va sur https://github.com et crée un compte (gratuit).
2. Bouton **New repository** → nom : `armure` → **Public** → « Create repository ».
3. Sur la page vide du dépôt : « uploading an existing file » → glisse tous les fichiers de ce dossier (pas le dossier lui-même, les fichiers dedans) → bouton vert « Commit changes ».
4. Onglet **Settings** du dépôt → menu **Pages** → sous « Build and deployment », Source : **Deploy from a branch** → Branch : `main` et `/ (root)` → « Save ».
5. Patiente 1 à 2 minutes, recharge la page : l'adresse de ton appli apparaît, du type
   `https://TON-PSEUDO.github.io/armure/`

## 5. Relier ton iPhone

1. Ouvre cette adresse dans **Safari** (pas dans Chrome, pas depuis une appli de messagerie).
2. L'écran « Première ouverture » s'affiche :
   - choisis un **code famille** secret et pas devinable, par ex. `armure-lucas-7h32` (au moins 6 caractères) ;
   - « Ce téléphone est celui de » → **Moi** ;
   - « Relier l'appli ».
3. Tu arrives sur l'accueil. Va dans **Suivi**, tout en bas, bloc **Réglages** : bouton **Envoyer par Messages / WhatsApp** (ou Copier) → envoie le lien à ta mère. Ce lien contient déjà la configuration et le code famille.

## 6. L'icône sur l'écran d'accueil (vous deux)

Sur chaque iPhone, dans Safari, avec l'appli ouverte :

1. Bouton **Partager** (le carré avec la flèche, en bas).
2. **Sur l'écran d'accueil** → « Ajouter ».

L'icône Armure apparaît. Elle s'ouvre en plein écran, sans barre Safari.
Ta mère : elle ouvre ton lien dans Safari (il la configure automatiquement en « Maman »), puis fait la même chose.

---

## Vérifier que ça marche

Toi : dans Repas, appuie sur une case « + » et propose un repas.
Elle : ouvre l'appli, le repas apparaît en jaune, elle appuie dessus et « Valider ».
Toi : la case passe en vert. C'est en place.

## Si ça bloque

- **« Connexion à Firebase impossible »** : la configuration collée est incomplète, ou Firestore n'a pas été créé (étape 1.3).
- **« Enregistrement refusé »** : les règles de l'étape 2 ne sont pas publiées, ou le mode test a expiré.
- **Page blanche** : attends 2 minutes après l'étape 4, puis recharge. Vérifie que `index.html` est bien à la racine du dépôt.
- **L'icône est une capture d'écran au lieu du logo** : tu as ajouté la page depuis Chrome ; refais-le depuis Safari.
- **Délier un téléphone** : Suivi → Réglages → « Délier ce téléphone ». Les données restent dans Firebase ; il suffit de rouvrir le lien.

## Mettre à jour l'appli plus tard

Quand je te donne une nouvelle version : sur GitHub, ouvre le dépôt → « Add file » → « Upload files » → remplace les fichiers → Commit. Sur les iPhone, ferme l'appli complètement et rouvre-la une ou deux fois.
