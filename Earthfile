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
    FROM node:26.3.1-alpine3.24
    WORKDIR /workspace
    RUN npm install -g renovate@latest
    COPY .github/renovate.json5 .github/renovate.json5
    RUN renovate-config-validator --strict .github/renovate.json5

# release builds and pushes the image for a specific OS
# this is meant to be run by a github workflow
release:
    FROM alpine:3.24.1@sha256:28bd5fe8b56d1bd048e5babf5b10710ebe0bae67db86916198a6eec434943f8b
    ARG --required OS
    BUILD --pass-args ./os/$OS+release
