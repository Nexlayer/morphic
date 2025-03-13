# Morphic

This repository is a fork of [miurla/morphic](https://github.com/miurla/morphic), enhanced with Nexlayer integration via a `nexlayer.yaml` configuration file.

1. [Nexlayer Updates to Repository](#nexlayer-updates-to-repository)
2. [Deploying to Nexlayer](#deploying-to-nexlayer)
3. [Accessing Your Deployment](#accessing-your-deployment)

## Nexlayer Updates to Repository

- `nexlayer.yaml` file added
- Github Actions workflow file (`nexlayer-deploy.yaml`) added to allow users to easily deploy the morphic application from their `nexlayer.yaml` file to Nexlayer.
- `Dockerfile-searxng` added to include the `searxng-setting.yml` in the SearXNG container image used in the `nexlayer.yaml` file.
- `/public/config/models.json` file updated to query the 1.5b model from deepseek-r1 for the `katieharris/ollama:deepseek-r1` image used in the `nexlayer.yaml` file.
- Github Actions workflow files (`docker-build-client.yaml` and `docker-build-searxng.yaml`) added to allow for rebuilding container images on changes to Morphic client code or updates to the `searxng-settings.yml` file (manual deployment only).

## Deploying to Nexlayer

Deploy your application to Nexlayer using one of these methods:

1. **Automatic Deployment**: Simply update the `nexlayer.yaml` file and push your changes.
2. **Manual Deployment**: Trigger the "Deploy on Nexlayer" workflow from the Actions tab.

## Accessing Your Deployment

1. Navigate to the **Actions** tab in this repository.
2. Locate the most recent "Deploy to Nexlayer" workflow run.
3. Click on the "curl-nexlayer" job.
4. Expand the "Show Response" section to view the Nexlayer API response.

If deployment is successful, you'll find a URL to your live application in the response.
