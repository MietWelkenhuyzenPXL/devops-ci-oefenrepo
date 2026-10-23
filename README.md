# Continious integration in Github actions
## Voorbereiding
Haal de code uit `https://github.com/PXL-2TIN-DevOps-Resources/calculator-app-finished` binnen en voeg deze toe aan deze repository.

In deze opdracht bouw je twee GitHub Actions-workflows die samen een eenvoudige CI-pipeline vormen voor onze applicatie:

- Deel 1: een kwaliteitsworkflow (`quality.yml`) die draait bij elk geopend pull request en codekwaliteit, formatting, secrets en unittests controleert.
- Deel 2: een CI-workflow (`ci.yml`) die bij pushes naar `main` (en handmatig via een knop) een Docker-image bouwt en naar Docker Hub pusht en het team verwittigt.

## Deel 1 - quality.yml
Trigger: [pull_request]

Vereiste stappen (je mag altijd stappen toevoegen indien nodig):

- Fetch code: checkout van de repository (gebruik actions/checkout).
- Check code quality: run ESLint. De workflow moet falen als ESLint fouten aanwezig zijn.
- Check code formatting: run Prettier (of een check-mode van Prettier). De workflow moet falen als formatting niet overeenkomt.
- Credential scan: voer een secrets-scan uit met trufflehog (trufflehog-oss of vergelijkbaar). De workflow moet falen bij gevonden secrets.
- Unittests: voer `npm test` uit. Verzamel testresultaten in een rapport (bijv. JUnit XML of een formaat dat een test-reporter ondersteunt).
- Archive / Upload reports: gebruik een test-reporter zodat de testrapporten zichtbaar zijn in de workflow-run of gekoppeld aan de PR. (Je kunt een marketplace action gebruiken om testresults in het Actions UI te tonen.)

Bouw een nieuwe feature in de applicatie aan de hand van de Github Flow. Deze gebruik je om aan te tonen dat de quality worfklow uitgevoerd wordt bij het openen van je Pull request. Je hoeft de pull request niet te mergen.

## Deel 2 - ci.yml 
Trigger: [push: { branches: [main] }, workflow_dispatch]

Vereiste stappen (je mag altijd stappen toevoegen indien nodig):

- Fetch code: checkout repository.
- Build docker image: bouw een image met als naam `<dockerhubUsername>/calculator-app` en tag `:<commit_hash>` (gebruik GITHUB_SHA of kort daarvan). 
- Push docker image: push de image naar DockerHub. Gebruik GitHub Secrets voor credentials.
- Notify team: stuur een notificatie naar een extern kanaal (eigen Discord server) met een bericht dat de nieuwe image is gepusht en een link naar de Dockerhub-repository. Gebruik een secret `DISCORD_WEBHOOK_URL` voor de webhook.

Voeg in onderstaande code block de url toe van je Dockerhub repository van de container:
```

```