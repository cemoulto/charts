# Running Buildkite agent builder

The [buildkite agent](https://buildkite.com/docs/agent) is a small, reliable and cross-platform build runner that makes it easy to run automated builds on your own infrastructure. Its main responsibilities are polling buildkite.com for work, running build jobs, reporting back the status code and output log of the job, and uploading the job's artifacts.

## TL;DR;

```bash
$ helm install clearbit/buildkite-builder --name bk-builder --namespace buildkite \
  --set agentToken="$(cat token)",agentMeta="role=builder-staging",privateSshKey="$(cat buildkite.key)",awsCreds="$(cat credentials)",workflowUserToken="$(cat client.json | base64)",workflowApiUrl="deis.my-domain.com"
```

## Introduction

This chart bootstraps a [buildkite agent](https://github.com/buildkite/docker-buildkite-agent) builder on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Get this chart

Clone the repo if you wish to use the development snapshot:

```bash
$ git clone https://github.com/clearbit/charts.git
```

## Installing the Chart

To install the chart with the release name `buildkite-builder`:

```bash
$ helm install --name bk-builder buildkite-builder-x.x.x.tg
```

*Replace the `x.x.x` placeholder with the chart release version.*

The command deploys buildkite agent on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `bk-builder` deployment:

```bash
$ helm delete bk-builder --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the `buildkite-builder` chart and their default values.

|     Parameter       |        Description             |               Default              |
|---------------------|--------------------------------|------------------------------------|
| `image`             | `buildkite/agent:latest` image | buildkite image latest tag         |
| `imagePullPolicy`   | Image pull policy              | `Always` if `imageTag` is `latest` |
| `agentTag`          | Agent release tag              | Must be specified                  |
| `dockerTag`         | Agent docker version tag       | Must be specified                  |
| `replicasCount`     | Replicas count                 | 1                                  |
| `agentToken`        | Agent token                    | Must be specified                  |
| `agentMeta`         | Agent role                     | `role=builder`                     |
| `privateSshKey`     | agent ssh key                  | Must be specified                  |
| `awsCreds`          | AWS credentials for ECR access | `nil`                                |
| `workflowUserToken` | Deis Workflow user token       | `nil`                                |
| `workflowApiUrl`    | Deis Workflow API URL          | `nil`                                |

## Buildkite pipeline example

Check for example of `pipeline.yml` and `build/deploy` scripts [here](pipeline-examples).
