Your research team needs to perform computationally intense data processing and doesn't have the equipment to do the work. They've decided to use Azure to do the data analysis.

## What is Azure compute?
Azure compute is an on-demand computing resource service for running cloud-based applications. It provides computing resources like multi-core processors and supercomputers via virtual machines and containers. It also provides serverless computing to enable running apps without requiring infrastructure setup or configuration. The resources are available on-demand and can typically be created in minutes or even seconds. You pay only for the resources you use and only for as long as you're using them.

There are three common techniques for performing compute in Azure:

- Virtual machines
- Containers
- Serverless computing

## What are virtual machines?

A **virtual machine (VM)** is a software emulation of a physical computer. They include a virtual processor, memory, storage, and networking resources. They host an operating system, and you're able to install and run software just like a physical computer. And by using a remote desktop client, you can use and control the virtual machine as if you were sitting in front of a physical terminal.

### Virtual machines in Azure

Virtual machines can be created and hosted in Azure. New virtual machines can typically be created and provisioned in minutes by selecting a pre-configured virtual machine image.

Selecting an image is one of the most important decisions you'll need to make when creating a VM. An image is a template used to create a virtual machine. These templates already include an operating system (OS) and often other software, such as development tools or web hosting environments.

## What are containers?

Containers are a virtualization environment but, unlike a virtual machine, they do not include an operating system. Instead, they reference the operating system of the host environment that runs the container. For example, if five containers are running on a server with a specific Linux kernel, all five containers are running on that same kernel.

The following illustration show a comparison between applications running directly on a VM and applications running inside containers on a VM.

![An illustration showing how the operating system is a part of the virtual machine and not part of the container.](../media/2-vm-versus-containers.png)

Containers typically contain an application that you write and will include any libraries required for your application to run on the host environment's kernel. 

Containers are meant to be lightweight and are designed to be created, scaled out, and stopped dynamically. This allows you to respond to changes in demand and quickly restart in case of a crash or hardware interruption. 

A benefit of using containers is the ability to run multiple isolated applications on a virtual machine. Since containers themselves are secured and isolated, you don't necessarily need separate VMs for separate workloads.

Azure supports Docker containers and several ways to manage those containers. Containers can be managed manually or with Azure services such as Azure Kubernetes Service.

### What is serverless computing?

Serverless computing is a cloud-hosted execution environment that runs your code but completely abstracts the underlying hosting environment. You create an instance of the service, and you add your code; no infrastructure configuration or maintenance is required, or even allowed.

You configure your serverless apps to respond to _events_. This could be a REST endpoint, a periodic timer, or even a message received from another Azure service. The serverless app runs only when it's triggered by an event.

Infrastructure isn't your responsibility. Scaling and performance are handled automatically, and you are billed only for the exact resources you use. There's no need to even reserve capacity.

Azure has two implementations of serverless compute: 

- **Azure Functions** which can execute code in almost any modern language
- **Azure Logic Apps** which are designed in a web-based designer and can execute logic triggered by Azure services without writing any code.
