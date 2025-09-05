# Pipeline v1alpha1 API

This directory contains the Kubernetes API definitions for the Tekton Pipelines v1alpha1 API.

## Purpose

This API allows users to define and manage pipelines, tasks, and other resources related to CI/CD workflows.

## Usage Examples

### Defining a Pipeline

```yaml
apiVersion: tekton.dev/v1alpha1
kind: Pipeline
metadata:
  name: my-pipeline
spec:
  tasks:
  - name: task1
    taskRef:
      name: my-task
```

### Defining a Task

```yaml
apiVersion: tekton.dev/v1alpha1
kind: Task
metadata:
  name: my-task
spec:
  steps:
  - name: step1
    image: ubuntu
    command: ['sh', '-c']
    args: ['echo Hello from step1']
```

## API Reference

For detailed information on each resource and its fields, refer to the generated OpenAPI specification: [swagger.json](swagger.json)
