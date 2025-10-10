VERSION --wildcard-builds 0.8

# test runs tests for for the given OS image (os/*/Earthfile) in this repo
test:
    ARG --required OS
    BUILD --pass-args ./os/$OS+test-build

# release expects to get a renovate branch in the form of renovate/<os>-dind-image, extracts the os and then kicks off its +release target
# this is meant to be run by a github workflow
release:
    FROM alpine:3.22.2@sha256:9eec16c5eada75150a82666ba0ad6df76b164a6f8582ba5cb964c0813fa56625
    # RENOVATE_BRANCH is the renovate branch that is expected to get merged and trigger this target
    ARG --required RENOVATE_BRANCH
    LET os=${RENOVATE_BRANCH#renovate/}
    # remove major-XX- or major-
    SET os=$(echo ${os#major-[[:digit:]]?-})
    SET os=${os#major-}
    # using a LET/SET in the target path does not work, use an ARG instead until it's fixed
    ARG OS=${os%-dind-image}
    BUILD --pass-args ./os/$OS+release
