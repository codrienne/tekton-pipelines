# Tekton Pipeline API v1alpha1

This directory contains the `v1alpha1` API definitions for Tekton Pipelines. This API group is considered alpha and may change in backward-incompatible ways.

## Custom Resources

The `v1alpha1` API group includes the following custom resources:

### Run

A `Run` represents a single execution of a Custom Task. Custom Tasks are a way to extend Tekton by integrating with other tools and services. A `Run` object references a `Task` (often a custom task) and provides the parameters and resources needed to execute it.

**Example `Run`:**

```yaml
apiVersion: tekton.dev/v1alpha1
kind: Run
metadata:
  name: my-custom-task-run
spec:
  ref:
    apiVersion: my-custom-task.example.com/v1
    kind: MyCustomTask
    name: my-custom-task
  params:
    - name: my-param
      value: "hello-world"
```

### StepAction

A `StepAction` represents a reusable, standalone action that can be referenced by a `Step` in a `Task`. This allows you to define common actions once and reuse them across multiple `Tasks`.

**Example `StepAction`:**

```yaml
apiVersion: tekton.dev/v1alpha1
kind: StepAction
metadata:
  name: my-step-action
spec:
  image: ubuntu
  command: ["echo"]
  args: ["Hello, World!"]
```

### VerificationPolicy

A `VerificationPolicy` defines rules for verifying the authenticity and integrity of Tekton resources. You can use it to specify which public keys should be used to verify signatures for resources from different sources.

**Example `VerificationPolicy`:**

```yaml
apiVersion: tekton.dev/v1alpha1
kind: VerificationPolicy
metadata:
  name: my-verification-policy
spec:
  resources:
    - pattern: "https://github.com/tektoncd/catalog.git"
  authorities:
    - name: "my-key"
      key:
        data: |
          -----BEGIN PUBLIC KEY-----
          ...
          -----END PUBLIC KEY-----
```
