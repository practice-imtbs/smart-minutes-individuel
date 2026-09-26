# IMT Smart Minutes : page d'envoi individuelle

Page d'envoi du service **PracTice** (IMT Business School) : déposez l'enregistrement d'une réunion,
recevez par e-mail le **compte rendu Word anonyme** et la **transcription** complète.

**→ https://practice-imtbs.github.io/smart-minutes-individuel/**

## Fonctionnement

1. Dès que vous collez **votre clé API Mistral**, la page la vérifie directement auprès de Mistral : l'envoi n'est possible qu'avec une clé valide.
2. La page envoie l'audio et la clé au serveur n8n du service PracTice, qui confirme la réception aussitôt.
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

## Votre clé Mistral

- Créez-la sur [console.mistral.ai](https://console.mistral.ai/api-keys) ; une [vidéo pas à pas](https://mediaserver.ip-paris.fr/permalink/v126d5d01ee484ud8y4x/) montre la marche à suivre. La transcription est facturée sur votre compte.
- Elle n'est envoyée qu'à Mistral (vérification) et au serveur n8n PracTice, qui ne la conserve ni ne la journalise.
- La page peut la **mémoriser dans votre navigateur** si vous cochez la case prévue (à éviter sur un
  ordinateur partagé). Le bouton « Oublier ma clé » l'efface.

## Technique

Page statique unique (`index.html`), sans dépendance ni collecte de données. Elle appelle le webhook
`https://n8n.srv1205184.hstgr.cloud/webhook/smart-minutes-page` (workflow « IMT Smart Minutes anonyme
Production », `QkZS0qB6w2yLCmdx`), qui n'accepte que les requêtes venant de `practice-imtbs.github.io`.
