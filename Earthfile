VERSION --wildcard-builds 0.8

# test runs tests for for the given OS image (os/*/Earthfile) in this repo
test:
    ARG --required OS
    BUILD --pass-args ./os/$OS+test-build

# release expects to get a renovate branch in the form of renovate/<os>-dind-image, extracts the os and then kicks off its +release target
# this is meant to be run by a github workflow
release:
    FROM alpine:3.23.4@sha256:5b10f432ef3da1b8d4c7eb6c487f2f5a8f096bc91145e68878dd4a5019afde11
    # RENOVATE_BRANCH is the renovate branch that is expected to get merged and trigger this target
    ARG --required RENOVATE_BRANCH
    LET os=${RENOVATE_BRANCH#renovate/}
    # remove major-XX- or major-
    SET os=$(echo ${os#major-[[:digit:]]?-})
    SET os=${os#major-}
    # using a LET/SET in the target path does not work, use an ARG instead until it's fixed
    ARG OS=${os%-dind-image}
    BUILD --pass-args ./os/$OS+release
