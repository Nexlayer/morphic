<div style="margin: 20px;">
  <img src="docs/images/nexlayer_lowercase.png" alt="Nexlayer GitHub Banner">
</div>

# Morphic

This repository is a fork of [miurla/morphic](https://github.com/miurla/morphic), enhanced with Nexlayer integration via a `nexlayer.yaml` configuration file.

1. [Deploying to Nexlayer](#deploying-to-nexlayer)
2. [Accessing Your Deployment](#accessing-your-deployment)

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
