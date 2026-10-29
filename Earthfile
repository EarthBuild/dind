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
    FROM node:26.13.0-alpine3.24@sha256:c6ad9e9c1d80f6eb607c26b4b0a132ff7a2344fad1c78ea3baa2a7d4c8de6d94
    WORKDIR /workspace
    RUN npm install -g renovate@latest
    COPY .github/renovate.json5 .github/renovate.json5
    RUN renovate-config-validator --strict .github/renovate.json5

# release builds and pushes the image for a specific OS
# this is meant to be run by a github workflow
release:
    FROM alpine:3.24.3@sha256:be2656061b536c1883c4034790e21d0a09c5aaaf51968b89368a3c0371ea2c9a
    ARG --required OS
    BUILD --pass-args ./os/$OS+release
