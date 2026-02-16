# Tekton Pipelines API v1beta1

This directory contains the `v1beta1` API definitions for Tekton Pipelines. The Custom Resource Definitions (CRDs) in this package are used to define and run CI/CD pipelines.

**Note:** The `v1beta1` API is deprecated. Please use the `v1` API instead.

## Custom Resource Definitions

The main CRDs in this package are:

*   **`Task`**: A `Task` is a collection of sequential `Steps` that are run as part of a `Pipeline`. Each `Step` is a container image that performs a specific action.
*   **`TaskRun`**: A `TaskRun` is an instantiation of a `Task`. It specifies the parameters and resources used to run the `Steps` in a `Task`.
*   **`Pipeline`**: A `Pipeline` is a collection of `Tasks` that are arranged in a directed acyclic graph (DAG). It defines the order in which `Tasks` are executed.
*   **`PipelineRun`**: A `PipelineRun` is an instantiation of a `Pipeline`. It specifies the parameters and resources used to run the `Tasks` in a `Pipeline`.

## Usage Examples

Here are some examples of how to use the `v1beta1` API.

### Task and TaskRun

This example shows a simple `Task` that prints "Hello, World!" and a `TaskRun` that executes it.

**`task.yaml`**
```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: hello-world
spec:
  steps:
    - name: echo
      image: ubuntu
      script: |
        #!/bin/bash
        echo "Hello, World!"
```

**`taskrun.yaml`**
```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: hello-world-run
spec:
  taskRef:
    name: hello-world
```

### Pipeline and PipelineRun

This example shows a `Pipeline` that contains a single `Task` and a `PipelineRun` that executes it.

**`pipeline.yaml`**
```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: hello-world-pipeline
spec:
  tasks:
    - name: hello-world-task
      taskRef:
        name: hello-world
```

**`pipelinerun.yaml`**
```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: hello-world-pipeline-run
spec:
  pipelineRef:
    name: hello-world-pipeline
```
