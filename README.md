# ci-scripts

Re-usable continuous integration (CI) scripts

Inspired by: https://circleci.com/blog/continuous-integration-at-segment/

Owned by `#eng-infra`.

## Scripts

### General-purpose

The following scripts don't rely on any Clever-specific tooling.

#### Docker

Logs into Docker registry, then builds and pushes docker image.
Docker image is tagged with 7 character git commit SHA.

```
$ ./circleci/docker-publish [DOCKER_USER] [DOCKER_PASS] [DOCKER_EMAIL] [ORG]
```

#### NPM Publish

Authenticates to NPM and publishes a package.

```
$ ./circleci/npm-publish [NPM_TOKEN] [PACKAGE_DIR]
```

#### Github Release

Publishes content from `[ARTIFACTS_DIR]` as a Github Release.

```
$ ./circleci/github-release [GITHUB_TOKEN] [ARTIFACTS_DIR]
```

### Clever internal

The following scripts depend on Clever-specific infrastructure and tooling.

#### Catapult

Publishes your application and build in [catapult](https://github.com/clever/catapult).

```
$ ./circleci/catapult-publish [CATAPULT_URL] [CATAPULT_USER] [CATAPULT_PASS] [APP_NAME]
```

If you need to publish multiple applications, run this command once for each.

#### Dapple

Deploys your application with [dapple](https://github.com/clever/dapple).
Requires that you've first pushed the Docker image and published the application to Catapult.

```
$ ./circleci/dapple-deploy <DAPPLE_URL> <DAPPLE_USER> <DAPPLE_PASS> <APP_NAME> [ENVIRONMENT] [DEPLOYMENT_STRATEGY]
```
**Note:** The default environment is `clever-dev` and the default deployment strategy is `confirm-then-deploy`.
Additionally you can choose a `no-confirm-deploy` strategy that does not require confirmation before deploying.


If you need to deploy multiple applications, run this command once for each.

#### Workflow

Publishes a workflow to [workflow-manager](https://github.com/clever/workflow-manager).

```
$ ./circleci/workflow-publish [WF_URL] [WF_USER] [WF_PASS] [WF_JSON]
```

#### Report-card

Disabled.

We still are keeping the script here so that repos that invoke it can do so safely.
But it is a no-op.
