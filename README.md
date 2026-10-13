# Unity — démarrage du vrai site (version initiale)

**Slogan :** Tout en un, plus proche de toi.
**Palette :** chocolat, crème, caramel doux.

## Ce qui fonctionne déjà
- Interface responsive téléphone/ordinateur.
- Sélecteur de langue : français, anglais, swahili, lingala, portugais et espagnol.
- Les libellés principaux de connexion et navigation changent avec la langue choisie.
- Création de compte et connexion Supabase une fois configuré.
- Lecture et création de publications partagées en ligne via Supabase.
- Affichage d'images depuis une URL publique.
- Mode démo local sans compte (les données ne sont pas partagées entre utilisateurs).

## Pour lancer Unity réellement
1. Crée un projet sur https://supabase.com/ (le plan gratuit convient au prototype).
2. Dans le tableau de bord Supabase, ouvre **SQL Editor** et exécute tout le contenu de `supabase-schema.sql`.
3. Dans **Project Settings → API**, copie l'URL du projet et la clé publique `anon`/`publishable`.
4. Dans `index.html`, remplace `CONFIG_URL = ''` et `CONFIG_ANON_KEY = ''` par ces valeurs. N'insère JAMAIS une clé `service_role` dans le navigateur.
5. Héberge le dossier avec un hébergeur de sites statiques (par exemple GitHub Pages ou Netlify). Pour GitHub Pages, pousse `index.html` et `supabase-schema.sql` dans un dépôt puis active Pages dans Settings.
6. Dans Supabase Authentication, configure les URL autorisées et l'URL de redirection pour ton domaine publié.

## Limites honnêtes de cette version
C'est une première version utilisable, mais pas encore un réseau social complet de production. Les messages privés, appels audio/vidéo, Stories réelles, téléversement de médias, commentaires, likes persistants, notifications, signalement/modération et anti-spam restent à développer. Avant une ouverture publique, prévoir tests, sauvegardes, règles de sécurité, confidentialité et modération.

## Fichiers
- `index.html` — interface et fonctions initiales.
- `supabase-schema.sql` — tables et règles d'accès de base.

## Accessibilité prévue
La version actuelle utilise une navigation simple, des boutons larges et une palette à contraste élevé. Avant le lancement public, il faudra encore tester avec des personnes de différents âges, ajouter des réglages de taille de texte, des descriptions accessibles aux lecteurs d'écran et vérifier soigneusement toutes les traductions.


## Récupération de compte et sécurité (prototype)
- Récupération par e-mail : le site utilise le flux `resetPasswordForEmail` de Supabase Auth.
- Récupération par SMS : le flux OTP est ajouté, mais **ne fonctionne réellement qu'après configuration d'un fournisseur SMS dans Supabase Auth** et vérification des numéros. Des frais SMS peuvent s'appliquer.
- L'utilisateur doit saisir un nouveau mot de passe après vérification du code.
- Ne jamais placer de clé `service_role` dans le code du navigateur. N'enregistre pas de mots de passe ni de codes SMS dans tes tables.
- Avant lancement public : configurer limites de tentatives/rate limiting, CAPTCHA si nécessaire, politique de mot de passe, protection anti-abus, e-mail confirmé, sessions, logs de sécurité, conditions de confidentialité et tests de récupération.
- Pour la sécurité, le numéro de téléphone ne doit pas être rendu public sur les profils. Prévoir une vérification de propriété du numéro avant de l'utiliser pour récupérer un compte.

**Important :** le formulaire de récupération n'envoie pas de vrais e-mails/SMS tant que les paramètres Supabase et les fournisseurs ne sont pas configurés. Les codes SMS ne sont pas un mécanisme magique de récupération sans vérification du numéro et configuration serveur.
