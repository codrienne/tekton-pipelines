# Tekton Pipelines API Version v1beta1

This directory contains the Go type definitions for version `v1beta1` of the Tekton Pipelines API.
The `v1beta1` API group provides a stable and feature-rich set of Custom Resource Definitions (CRDs) for defining and running CI/CD pipelines on Kubernetes.

## Core Concepts

The Tekton Pipelines API is built around three main concepts: `Task`, `Pipeline`, and `PipelineRun`.

### Task

A `Task` is a collection of sequential `steps` that are run as part of a `Pipeline`. Each `step` is a container image that performs a specific action, such as building code, running tests, or deploying an application. `Tasks` can have input and output parameters, as well as workspaces for sharing data between `steps`.

**Example `Task`:**

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: hello-world
spec:
  params:
    - name: username
      description: The name to say hello to.
      default: "World"
  steps:
    - name: echo
      image: ubuntu
      script: |
        #!/bin/bash
        echo "Hello, $(params.username)!"
```

### Pipeline

A `Pipeline` is a collection of `Tasks` that are arranged in a specific order of execution. `Pipelines` define how the output of one `Task` can be used as the input to another, allowing you to create complex CI/CD workflows.

**Example `Pipeline`:**

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: hello-world-pipeline
spec:
  params:
    - name: username
      description: The name to say hello to.
  tasks:
    - name: say-hello
      taskRef:
        name: hello-world
      params:
        - name: username
          value: $(params.username)
```

### PipelineRun

A `PipelineRun` is an instance of a `Pipeline` that is being executed. It specifies the `Pipeline` to run and provides the necessary input parameters and resources. Creating a `PipelineRun` will trigger the execution of the `Pipeline` and create `TaskRuns` for each `Task` in the `Pipeline`.

**Example `PipelineRun`:**

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: hello-world-pipeline-run
spec:
  pipelineRef:
    name: hello-world-pipeline
  params:
    - name: username
      value: "Tekton"
```

By using these CRDs, you can define and manage your CI/CD pipelines as code, and leverage the power of Kubernetes to run them in a scalable and reliable way.
