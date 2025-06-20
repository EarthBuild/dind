# Earthly dind (Docker In Docker) Images
[![Release](https://github.com/earthly/dind/actions/workflows/release.yml/badge.svg)](https://github.com/earthly/dind/actions/workflows/release.yml)
![Docker Pulls](https://img.shields.io/docker/pulls/earthly/dind)


Earthly's official [earthly/dind](https://hub.docker.com/repository/docker/earthly/dind/general) docker images.
For information on how to use these images, please refer to [docker in earthly](https://docs.earthly.dev/docs/guides/docker-in-earthly).

## Supported Distributions

There are currently 4 supported dind distributions available:
- `alpine`
- `ubuntu:20.04`
- `ubuntu:23.04`
- `ubuntu:24.04`

Other distributions and/or base images can be used with our [dind+INSTALL](https://docs.earthly.dev/docs/guides/docker-in-earthly#performance) [FUNCTION](https://docs.earthly.dev/docs/guides/functions).

## How Images are Built

In this repository, we maintain the OS & Docker versions that warrants releasing a new version of the image.
However, the installations of docker and other dependencies are done via an installation script that is currently maintained in [earthly/earthly](https://github.com/earthly/earthly).

### Dependencies

Dependencies are maintained by Renovate and will be merged automatically (provided required checks pass), primarly
dependencies that will trigger new versions of the dind images such as the docker or the os (alpine) versions.

## Repo structure

```bash
.
├── Earthfile // Targets that apply to all images (e.g. +test)
├── common
│   └── Earthfile // A library of common helper targets
└── os // Each directory contains an Earthfile with targets to maintain the specific os (e.g. +test, +build)
    ├── alpine
    │   └── Earthfile
    ├── ubuntu-20.04
    │   └── Earthfile
    └── ubuntu-23.04
        └── Earthfile
    └── ubuntu-24.04
        └── Earthfile
```

## Testing

Images are tested by running remote test targets that are maintained in [earthly/earthly](https://github.com/earthly/earthly/tree/main/tests/with-docker). This is because these tests also help test [WITH DOCKER](https://docs.earthly.dev/docs/earthfile#with-docker) command in earthly cli.

Temporary images are built, pushed, and pulled as part of the test cycle.

### How to run tests

* Test a specific image os:

```bash
earthly --push -P ./os/<os>+test-build
```

* Test all images:
```bash
earthly --push -P +test
```

#### Community members

Community members do not have permissions to push a built image and run the tests against it. However, they can easily set a different container registry repository by changing the `CR_HOST` (default: ghcr.io) and `CR_ORG` ARG values in [.arg](.arg) to a private container registry repository or by passing the args in the earthly command, e.g. `earthly --push -P +test --CR_HOST=<your-container-registry> --CR_ORG=<your-organization>`.

## Deployment

When the relevant dependencies are updates by Renovate, new images/tags will be pushed automatically to the docker registry.

## Contributing

* Please report bugs as [GitHub issues](https://github.com/earthly/dind/issues).
* Join us on [Slack](https://earthly.dev/slack)!
* Questions via GitHub issues are welcome!
* PRs welcome! But please give a heads-up in a GitHub issue before starting work. If there is no GitHub issue for what you want to do, please create one.
* Check the [contributing page](./CONTRIBUTING.md) for more details.

## Licensing

Earthly is licensed under the Mozilla Public License Version 2.0. See [LICENSE](./LICENSE).
