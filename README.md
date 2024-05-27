# kaniko-documentation
Kaniko is a tool used to build container images from a Dockerfile inside a Kubernetes cluster or any environment where a Docker daemon is not available. It does this securely and efficiently without requiring root privileges. When running Kaniko, three key arguments are commonly required:

### `--dockerfile`

- **Description**: Specifies the path to the Dockerfile that Kaniko should use to build the image.
- **Example**: `--dockerfile=/path/to/Dockerfile`

### `--context`

- **Description**: Defines the build context, which is the directory containing the Dockerfile and any files required for building the Docker image.
- **Example**: `--context=dir:///path/to/build/context` for a local directory or `--context=gs://bucket/path` for a Google Cloud Storage bucket.

### `--destination`

- **Description**: Indicates the destination where the built image will be pushed. This is typically a container registry.
- **Example**: `--destination=gcr.io/project-id/image-name:tag` for Google Container Registry, or `--destination=docker.io/username/image-name:tag` for Docker Hub.
