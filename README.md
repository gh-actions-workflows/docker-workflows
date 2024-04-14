# Docker Workflow

Construa a sua imagem Docker e publique-a no DockerHub.

## Como utilizar?

```yaml
name: Publish Docker Image
on: [push]

jobs:
    publish:
      uses: PedroHPAlmeida/actions-workflows-docker/.github/workflows/docker-publish.yaml@master
      if: ${{ github.ref_name == 'master' || github.ref_name == 'develop'}} # Opcional
      with:
        app_name: app-name # O nome da aplicação será usado para nomear a imagem
        docker_hub_user: ${{ vars.DOCKER_HUB_USER }}
      secrets:
        docker_hub_password: ${{ secrets.DOCKER_HUB_PASSWORD }}
```

## Outputs

* **image_name**: nome e tag da imagem publicada.

## Observações

* O nome da imagem seguirá o seguinte padrão **DOCKER_HUB_USER/APP_NAME**. É necessário colocar o usuário no início do nome para fazer a publicação no DockerHub.
* A tag da imagem seguirá o seguinte padrão: **BRANCH_NAME-COMMIT_SHA**. O nome da branch em que o workflow está sendo executado (e.g. develop, release, master), e o sha do útimo commit.

Para mais detalhes sobre o funcionamento consulte o arquivo: [docker-publish.yaml](https://github.com/PedroHPAlmeida/actions-workflows-docker/blob/master/.github/workflows/docker-publish.yaml).
