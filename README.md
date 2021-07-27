# Buildah Build&Push Action

> This action is highly specific for a few Portworx-internal repositories - may not be suited for generic usage.

Runs a `buildah.sh` script in a specified directory. The script is expected to produce a buildah image and commit it with the same name as the name of the containing directory.
This image is then pushed to a specified container registry.

## Usage

```yml
- uses: portworx/action-buildah-build-push@v1
  with:
    image-name: portworx/image
    image-tag: tag
    short-sha: 6f9kl1d
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}
```

## Inputs

```yml
remote-registry:
  description: 'Name of the remote registry to push to.'
  required: true
  default: 'docker.io'

image-name:
  description: 'Name of the image. This should correspond to the name of the repository which will be pushed to.'
  required: true

image-tag:
  description: 'Tag of the image. This should also correspond to the containing directory name. The resulting tag will use this name.'
  required: true

short-sha:
  description: 'Short git SHA of the current commit. This will be appended to the pushed image tag.'
  required: true

username:
  description: 'Username used for authentication to the target registry.'
  required: true

password:
  description: 'Password used for authentication to the target registry.'
  required: true
```

## Outputs

```yml
image-path:
    description: 'Full path to the image pushed to the remote registry.'
    value: ${{ steps.push.outputs.image-path }}
```
