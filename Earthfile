VERSION --wildcard-builds 0.8

# test runs tests for for the given OS image (os/*/Earthfile) in this repo
test:
    ARG --required OS
    BUILD --pass-args ./os/$OS+test-build

# lint runs all lint targets
lint:
    BUILD +lint-renovate

# lint-renovate validates the Renovate configuration file
lint-renovate:
    FROM node:26.10.0-alpine3.24@sha256:0b36e8c136b94cd4fcf02188228e76c31ad5872eef3fec8cbd2eee500cfd9e80
    WORKDIR /workspace
    RUN npm install -g renovate@latest
    COPY .github/renovate.json5 .github/renovate.json5
    RUN renovate-config-validator --strict .github/renovate.json5

# release builds and pushes the image for a specific OS
# this is meant to be run by a github workflow
release:
    FROM alpine:3.24.2@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6
    ARG --required OS
    BUILD --pass-args ./os/$OS+release
