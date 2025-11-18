# Tekton Pipelines API Version 1

This directory contains the Go type definitions for version `v1` of the Tekton Pipelines API.

The Tekton Pipelines API is composed of several Custom Resource Definitions (CRDs) that allow users to define and run CI/CD pipelines in Kubernetes.

## Core Concepts

The main CRDs defined in this package are:

*   **`Task`**: Represents a collection of sequential steps that are run as part of a pipeline. Each step is a container image that performs a specific action.
*   **`TaskRun`**: Represents a single execution of a `Task`. It specifies the parameters and resources used to run the steps in a `Task`.
*   **`Pipeline`**: Represents a graph of `Tasks` that are executed in a specific order. It defines how the outputs of one `Task` are passed as inputs to another `Task`.
*   **`PipelineRun`**: Represents a single execution of a `Pipeline`. It specifies the parameters and resources used to run the `Tasks` in a `Pipeline`.

## Usage Example

Here is a simple example of how to define a `Task` and a `TaskRun` using the Go types from this package:

```go
import (
	"github.com/tektoncd/pipeline/pkg/apis/pipeline/v1"
	corev1 "k8s.io/api/core/v1"
	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
)

func main() {
	// Create a new Task
	task := &v1.Task{
		ObjectMeta: metav1.ObjectMeta{
			Name: "hello-world",
		},
		Spec: v1.TaskSpec{
			Steps: []v1.Step{
				{
					Name:    "echo",
					Image:   "ubuntu",
					Command: []string{"echo"},
					Args:    []string{"Hello, World!"},
				},
			},
		},
	}

	// Create a new TaskRun to execute the Task
	taskRun := &v1.TaskRun{
		ObjectMeta: metav1.ObjectMeta{
			Name: "hello-world-run",
		},
		Spec: v1.TaskRunSpec{
			TaskRef: &v1.TaskRef{
				Name: "hello-world",
			},
		},
	}
}
```

For more information about the Tekton Pipelines API, please refer to the official [Tekton documentation](https://tekton.dev/docs/).
