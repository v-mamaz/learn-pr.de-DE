Azure Container Registry is a managed Docker registry service based on the open-source Docker Registry 2.0. Container Registry is a private, hosted in Azure, and allows you to build, store, and manage images for all types of container deployments.

Container images can be pushed and pulled with Container Registry using the Docker CLI or the Azure CLI. Azure portal integration allows you to visually inspect the container images in your container registry. In distributed environments, the Container Registry geo-replication feature can be used to distribute container images to multiple Azure datacenters for localized distribution.

In addition to storing container images, Azure Container Registry Build can build container images in Azure. Build uses a standard Dockerfile to create and store a container image in Azure Container Registry without the need for local Docker tooling. With Azure Container Registry Build, you can build on demand or fully automate container image builds using DevOps processes and tooling.

## Learning objectives

In this module, you will:

- Deploy an Azure container registry
- Build a container image using Azure Container Registry Build
- Deploy this container to an Azure container instance
- Replicate the container image to multiple Azure datacenters