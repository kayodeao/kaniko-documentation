# kaniko-documentation
Kaniko is a tool used to build container images from a Dockerfile inside a Kubernetes cluster or any environment where a Docker daemon is not available. It does this securely and efficiently without requiring root privileges. 

## Prerequisites for Kaniko

Before using Kaniko, ensure you have the following prerequisites:

1. **Kubernetes Cluster (Optional)**:
   - If running Kaniko in a Kubernetes cluster, ensure you have a functional Kubernetes cluster and `kubectl` configured to interact with it.

2. **Kaniko Executor Image**:
   - You need the Kaniko executor image, which is available from Google Container Registry or Docker Hub. The typical image is `gcr.io/kaniko-project/executor`.

3. **Build Context**:
   - A build context, which includes the Dockerfile and any necessary files for building the image. This context can be a local directory, a Google Cloud Storage bucket, or any other supported storage.

4. **Container Registry Access**:
   - Access to a container registry where the built image will be pushed. This could be Docker Hub, Google Container Registry, Amazon ECR, or any other supported registry.

5. **Credentials for Container Registry**:
   - Appropriate credentials to push images to your container registry. This may involve setting up service account keys for Google Container Registry, AWS credentials for Amazon ECR, or Docker credentials for Docker Hub.


For detailed setup instructions and more information, refer to the [Kaniko Documentation](https://github.com/GoogleContainerTools/kaniko#kaniko-build-contexts).

When running Kaniko, three key arguments are commonly required:
### `--dockerfile`

- **Description**: Specifies the path to the Dockerfile that Kaniko should use to build the image.
- **Example**: `--dockerfile=/path/to/Dockerfile`

### `--context`

- **Description**: Defines the [Build Contexts](https://github.com/GoogleContainerTools/kaniko#kaniko-build-contexts), which is the directory containing the Dockerfile and any files required for building the Docker image.
- **Example**: `--context=dir:///path/to/build/context` for a local directory or `--context=gs://bucket/path` for a Google Cloud Storage bucket.

### `--destination`

- **Description**: Indicates the destination where the built image will be pushed. This is typically a container registry.
- **Example**: `--destination=gcr.io/project-id/image-name:tag` for Google Container Registry, or `--destination=docker.io/username/image-name:tag` for Docker Hub.

# Running Kaniko in a Kubernetes Cluster to Push Images to Docker Hub

## Prerequisites

1. **Kubernetes Cluster**: Ensure you have a running Kubernetes cluster and `kubectl` is configured to interact with it.
2. **Docker Hub Account**: Have a Docker Hub account and obtain your Docker Hub credentials (username and password).
3. **Kaniko Executor Image**: Use the Kaniko executor image from Google Container Registry.

## Steps

### 1. Create a Kubernetes Secret for Docker Hub Credentials

First, create a Kubernetes secret to store your Docker Hub credentials. Replace `<your-docker-username>` and `<your-docker-password>` with your actual Docker Hub username and password.

```sh
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=kunchalavikram --docker-password=<your-pword> --docker-email=<your-email>
```
### 2. Create a Kaniko Pod Manifest
Create a YAML file (e.g., kaniko-pod.yaml) with the following content. This configuration will use the Kaniko executor to build the image and push it to Docker Hub:
```sh
nano kaniko-pod.yaml
```
*copy and paste the example-o1-githubcontext(public).yaml*

### 3. Deploy the Kaniko Pod:
```sh
kubectl apply -f kaniko-pod.yaml
```
### 4. Monitor the Kaniko Pod:
```sh
kubectl get pods
kubectl logs kaniko
```



# Conclusion

With Kaniko, developers can seamlessly integrate container image building into their Kubernetes workflows without the need for Docker daemons or privileged access, making it an efficient and secure choice for CI/CD pipelines and development environments.



