[![Release](https://github.com/earthbuild/dind/actions/workflows/release.yml/badge.svg)](https://github.com/earthbuild/dind/actions/workflows/release.yml) ![Docker Pulls](https://img.shields.io/docker/pulls/earthbuild/dind)

# EarthBuild Docker In Docker (dind) Images

The `dind` (docker-in-docker) image is designed for EarthBuild targets that use the `WITH DOCKER` command.

For information on how to use these images, please refer to [docker in EarthBuild](https://docs.earthly.dev/docs/guides/docker-in-earthly).

## Supported Distributions

This image supports the following Linux distributions:
* alpine
* ubuntu:20.04
* ubuntu:23.04
* ubuntu:24.04

For which the current latest tags (respectively) are:
* `alpine-3.22-docker-28.3.3-r0`
* `ubuntu-20.04-docker-28.1.1-1`
* `ubuntu-23.04-docker-25.0.2-1`
* `ubuntu-24.04-docker-28.3.3-1`

For other available tags, please check out [ghcr.io/earthbuild/dind](https://github.com/earthbuild/dind/pkgs/container/dind/versions?filters%5Bversion_type%5D=tagged) or [earthbuild/dind](https://hub.docker.com/r/earthbuild/dind/tags).

