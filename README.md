# IMT Smart Minutes : page d'envoi individuelle

Page d'envoi du service **PracTice** (IMT Business School) : déposez l'enregistrement d'une réunion,
recevez par e-mail le **compte rendu Word anonyme** et la **transcription** complète.

**→ https://practice-imtbs.github.io/smart-minutes-individuel/**

## Fonctionnement

1. Vous saisissez votre **adresse e-mail de l'école** : le service est réservé aux adresses `@imt-bs.eu` et `@imtbs-tsp.eu`. Aucune clé API n'est demandée.
2. La page envoie l'audio au serveur n8n du service PracTice, qui confirme la réception aussitôt et revérifie l'adresse.
3. L'audio est découpé en tranches de 15 minutes, transcrit par Mistral Voxtral avec séparation des voix,
   les voix sont réunies d'une tranche à l'autre, puis le compte rendu est rédigé par ILaaS.
4. Le compte rendu (.docx) et la transcription (.txt) arrivent par e-mail depuis `practice@imt-bs.eu`.

## Compte rendu anonyme

Personne n'est nommé automatiquement : deviner qui parle à partir de la voix produisait trop d'erreurs
d'attribution. Les personnes sont désignées par « Participant 1 », « Participant 2 »… (par temps de parole
décroissant). En tête du Word, l'encadré **« Qui est qui ? »** cite une ou deux phrases réellement prononcées
par chacune ; vous remplacez ensuite les étiquettes par les vrais noms avec Rechercher et remplacer
(Ctrl+H, option « Mot entier »). Les « personnes présentes » saisies dans la page n'apparaissent que dans
l'en-tête, jamais associées aux propos.

## Prise en charge

La transcription utilise la clé Mistral du service PracTice, conservée sur le serveur n8n et jamais dans la page.
Le service tient un décompte anonyme de l'usage (date, domaine de l'adresse, durée de l'audio), sans titre,
nom ni contenu. Merci d'en faire un usage raisonnable.

## Technique

Page statique unique (`index.html`), sans dépendance ni collecte de données. Elle appelle le webhook
`https://n8n.srv1205184.hstgr.cloud/webhook/smart-minutes-service` (workflow « IMT Smart Minutes service »,
`f2vRe5b5AqHHdQEz`), qui n'accepte que les requêtes venant de `practice-imtbs.github.io`.
