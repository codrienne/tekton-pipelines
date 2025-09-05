# Tekton Pipelines v1 API

This directory contains the API schema definitions for the `tekton.dev/v1` API group, which is the stable version of the Tekton Pipelines API. These Go types are used to define and manage Continuous Integration and Continuous Delivery (CI/CD) pipelines on Kubernetes.

## Key Concepts and Types

The core types defined in this package include:

*   **`Pipeline`**: Defines a series of `Tasks` to be executed in a specific order, often with dependencies between them.
*   **`PipelineRun`**: Represents a single execution of a `Pipeline`.
*   **`Task`**: Defines a set of steps (container images) to be executed, along with inputs, outputs, and workspaces.
*   **`TaskRun`**: Represents a single execution of a `Task`.
*   **`CustomRun`**: Allows for the integration of custom tasks or operations not natively supported by Tekton.
*   **`Resolution`**: Defines how external resources (like Git repositories or OCI images) are resolved.
*   **`Workspace`**: Represents a volume that can be shared between `Tasks` within a `Pipeline` or `TaskRun`.
*   **`Param`**: Defines parameters that can be passed to `Tasks` or `Pipelines`.
*   **`Result`**: Defines results that can be emitted by `Tasks` and consumed by subsequent `Tasks` or `Pipelines`.
*   **`WhenExpression`**: Allows for conditional execution of `Tasks` or `Steps` based on certain conditions.
*   **`Artifact`**: Represents inputs or outputs of `Tasks`, such as source code or build images.

## Purpose

These API types enable users to:
*   Define reusable `Tasks` and `Pipelines`.
*   Execute `Pipelines` and `Tasks` on Kubernetes clusters.
*   Manage the lifecycle of CI/CD workflows.
*   Integrate with various tools and services through custom tasks and resolvers.

## Usage Example (Conceptual)

While the full YAML definitions are extensive, here's a conceptual overview of how a `Task` and `TaskRun` might be structured:

```go
// A Task defines a series of steps to be executed.
type Task struct {
    metav1.TypeMeta   `json:",inline"`
    metav1.ObjectMeta `json:"metadata,omitempty"`
    Spec              TaskSpec   `json:"spec,omitempty"`
    Status            TaskStatus `json:"status,omitempty"`
}

// TaskSpec defines the desired state of a Task.
type TaskSpec struct {
    // Params are parameters that a user can provide to a Task
    Params []ParamSpec `json:"params,omitempty"`
    // Steps are the sequential list of steps that are executed in a Task.
    Steps []Step `json:"steps,omitempty"`
    // Workspaces are the volumes that a Task requires.
    Workspaces []WorkspaceDeclaration `json:"workspaces,omitempty"`
    // Results are the results that a Task can emit.
    Results []TaskResult `json:"results,omitempty"`
}

// A TaskRun represents a single execution of a Task.
type TaskRun struct {
    metav1.TypeMeta   `json:",inline"`
    metav1.ObjectMeta `json:"metadata,omitempty"`
    Spec              TaskRunSpec   `json:"spec,omitempty"`
    Status            TaskRunStatus `json:"status,omitempty"`
}

// TaskRunSpec defines the desired state of a TaskRun.
type TaskRunSpec struct {
    // TaskRef is a reference to a Task.
    TaskRef *TaskRef `json:"taskRef,omitempty"`
    // Params are parameters that a user can provide to a TaskRun.
    Params []Param `json:"params,omitempty"`
    // Workspaces are the volumes that a TaskRun requires.
    Workspaces []WorkspaceBinding `json:"workspaces,omitempty"`
}
```

For detailed YAML examples and further documentation, please refer to the official Tekton Pipelines documentation.
