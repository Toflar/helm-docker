# helm-docker

[![Docker Pulls](https://img.shields.io/docker/pulls/devth/helm.svg?style=flat-square)](https://hub.docker.com/r/devth/helm/)

## Usage

This Docker image includes `helm` along with:

- `gcloud`
- `kubectl`
- `envsubst`

And `helm` plugins:

- `viglesiasce/helm-gcs.git`
- `databus23/helm-diff`

## Docker

Docker images are automatically built on [Docker
Hub](https://hub.docker.com/r/devth/helm/):

- Docker tags correspond to [Helm
  release](https://github.com/helm/helm/releases) versions.
- `latest` is always the latest fully released version (non-RC).

### Building

```bash
docker build -t devth/helm .
```

## Release procedure

1. Bump `VERSION` in the [Dockerfile](Dockerfile)
1. Commit and create tag matching the version:

   ```bash
   VERSION=v2.12.3
   ISSUE=38
   git commit -am "Bump to $VERSION; fix #$ISSUE"
   git tag $VERSION
   git push && git push --tags
   ```

### Re-release

To re-build a particular tag we need to delete the git tag locally and remotely:

```bash
git push origin :$VERSION
git tag -d $VERSION
```

Then re-tag and push:

```bash
git tag $VERSION
git push --tags
```
