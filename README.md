# travis-test
https://travis-ci.org/

## Getting started
1. Add `.travis.yml` fro Travis CI
1. Selecting a language from [full list](https://docs.travis-ci.com/user/languages/)
1. Selecting infrastructure (optional) - default container: `Ubuntu 12.04`
1. Running test or [doing more stuff](https://docs.travis-ci.com/user/getting-started/#More-than-running-tests)

## Customizing the Build

### The Build Lifecycle

Build steps

1. OPTIONAL Install `apt addons`

    Depend on the project language

1. OPTIONAL Install `cache components`
1. `before_install`
1. `install`
1. `before_script`
1. `script`
1. OPTIONAL `before_cache` (for cleaning up cache)
1. `after_success` or `after_failure`
1. OPTIONAL `before_deploy`
1. OPTIONAL `deploy`
1. OPTIONAL `after_deploy`
1. `after_script`

### Customizing the Installation Step
Depends on the project language

###
Skipping the Installation Step

```yaml
    install: true
```

## Customizing the Build Step
Depends on the project language

## Deploying your Code
Preventing Travis CI from resetting your working directory and deleting all changes made during the build.
```yaml
deploy:
  skip_cleanup: true
```

## Build Timeouts
A job is way to long.

## Limiting Concurrent Builds
Set maximum number of concurrent builds from each repository.

## Building only the latest commit
By `Auto Cancellation Setting`

## Building Specific Branches

```yaml
# blocklist
branches:
  except:
  - legacy
  - experimental

# safelist
branches:
  only:
  - master
  - stable
```

## Build Matrix

56 individual (7 * 4 * 2) jobs.
```yaml
rvm:
  - 1.9.3
  - 2.0.0
  - 2.2
  - ruby-head
  - jruby
  - rbx-2
  - ree
gemfile:
  - gemfiles/Gemfile.rails-2.3.x
  - gemfiles/Gemfile.rails-3.0.x
  - gemfiles/Gemfile.rails-3.1.x
  - gemfiles/Gemfile.rails-edge
env:
  - ISOLATED=true
  - ISOLATED=false
```

## Implementing Complex Build Steps
Using shell script to setup complex build environment.

```sh
#!/bin/bash
set -ev
bundle exec rake:units
if [ "${TRAVIS_PULL_REQUEST}" = "false" ]; then
    bundle exec rake test:integration
fi
```

## Custom Hostnames
Travis CI will set the hostname in `/etc/hosts`

```yaml
addons:
  hosts:
  - travis.dev
  - joshkalderimis.com
```

## What repository providers or version control systems can I use?
GitHub only.