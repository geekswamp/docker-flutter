[![Publish Registry to ghcr.io](https://github.com/geekswamp/docker-flutter/actions/workflows/publish.yaml/badge.svg?branch=main)](https://github.com/geekswamp/docker-flutter/actions/workflows/publish.yaml)

# Docker Flutter

You can run it using CI or locally via Docker.

# Usage
## Dockerfile

Use as base image in `Dockerfile`

```Dockerfile
FROM ghcr.io/geekswamp/flutter:stable
```
## GitLab CI

Use as base image in `.gitlab-ci.yml`

```yml
image: ghcr.io/geekswamp/flutter:stable

stages:
  - build

build:
  stage: build
  ...
```