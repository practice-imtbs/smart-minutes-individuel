# IMT Smart Minutes : page d'envoi individuelle

Page d'envoi du service **PracTice** (IMT Business School) : déposez l'enregistrement d'une réunion,
recevez par e-mail le **compte rendu Word** et la **transcription** complète.

**→ https://practice-imtbs.github.io/smart-minutes-individuel/**

## Fonctionnement

1. La page envoie l'audio et **votre clé API Mistral** au serveur n8n du service PracTice.
2. La clé est vérifiée auprès de Mistral avant tout traitement ; une clé refusée n'engage rien.
3. L'audio est découpé en tranches de 15 minutes, transcrit par Mistral Voxtral avec séparation des voix,
   les voix sont réunies d'une tranche à l'autre, puis le compte rendu est rédigé par ILaaS.
4. Le compte rendu (.docx) et la transcription (.txt) arrivent par e-mail depuis `practice@imt-bs.eu`.

## Votre clé Mistral

- Créez-la sur [console.mistral.ai](https://console.mistral.ai/api-keys). La transcription est facturée sur votre compte.
- Elle n'est envoyée qu'au serveur n8n PracTice, qui ne la conserve ni ne la journalise.
- La page peut la **mémoriser dans votre navigateur** si vous cochez la case prévue (à éviter sur un
  ordinateur partagé). Le bouton « Oublier ma clé » l'efface.

## Technique

Page statique unique (`index.html`), sans dépendance ni collecte de données. Elle appelle le webhook
`https://n8n.srv1205184.hstgr.cloud/webhook/smart-minutes-page` (workflow « IMT Smart Minutes individuel
Production »), qui n'accepte que les requêtes venant de `practice-imtbs.github.io`.
