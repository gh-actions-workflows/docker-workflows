# Docker Workflow

Build your Docker image and publish it to DockerHub.

## How to use?

```yaml
name: Publish Docker Image
on: [push]

jobs:
    publish:
      uses: gh-actions-workflows/docker-workflows/.github/workflows/docker-publish.yaml@master
      if: ${{ github.ref_name == 'master' || github.ref_name == 'develop'}} # Optional
      with:
        app_name: app-name # The application name will be used to name the image
        docker_hub_user: ${{ vars.DOCKER_HUB_USER }}
      secrets:
        docker_hub_password: ${{ secrets.DOCKER_HUB_PASSWORD }}
```

## Outputs

* **image_name**: name and tag of the published image.

## Notes

* The image name will follow the following pattern **DOCKER_HUB_USER/APP_NAME**. You must put the user at the beginning of the name to publish to DockerHub.
* The image tag will follow the following pattern: **BRANCH_NAME-COMMIT_SHA**. The name of the branch in which the workflow is being executed (e.g. develop, release, master), and the sha of the last commit.

For more details on how it works, see the file: [docker-publish.yaml](https://github.com/gh-actions-workflows/docker-workflows/blob/master/.github/workflows/docker-publish.yaml).
