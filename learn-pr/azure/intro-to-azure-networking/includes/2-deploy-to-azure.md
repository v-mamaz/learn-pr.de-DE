Your first step will likely be to re-create your on-premises configuration in the cloud.

This basic configuration will give you a sense of how networks are configured, and how network traffic moves in and out of Azure.

## Your e-commerce site at a glance

Larger enterprise systems are often composed of multiple inter-connected applications and services that work together. You might have a front-end web system that takes displays inventory and allows customers to create an order. That might talk to a variety of web services to provide the inventory data, manage user profiles, process credit cards, and request fulfillment of processed orders.

There are several strategies and patterns employed by software architects and designers to make these complex systems easier to design, build, manage, and maintain. Let's look at a few of them, starting with _loosely coupled architectures_.

### Benefits of a loosely coupled architecture

<!-- TOOD: verify video -->
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2yHrc]

### Using an N-tier architecture

An architectural pattern that can be used to build loosely coupled systems is _N-Tier_.

An [N-tier architecture](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) divides an application into two or more logical tiers. Architecturally, a higher tier can access services from a lower tier, but a lower tier should never access a higher tier.

Tiers help separate concerns, and are ideally designed to be reusable. Using a tiered architecture also simplifies maintenance. Tiers can be updated or replaced independently, and new tiers can be inserted if needed.

_Three-tier_ refers to an n-tier application that has three tiers. Your e-commerce web application follows this three-tier architecture:

* The **web tier** provides the web interface to your users through a browser.
* The **application tier** runs business logic.
* The **data tier** includes databases and other storage that hold product information and customer orders.

The following illustration shows the flow of request from the user to the data tier.

![An illustration showing a three-tier architecture where each tier is hosted in a dedicated virtual machine.](../media/2-three-tier.png)

When the user clicks the button to place the order, the request is sent to the web tier, along with the user's address and payment information. The web tier passes this information to the application tier, which would validate payment information and check inventory. The application tier might then store the order in the data tier, to be picked up later for fulfillment.

## Your e-commerce site running on Azure

Azure provides many different ways to host your web applications, from fully pre-configured environments that host your code, to virtual machines that you configure, customize, and manage.

Let's say you choose to run your e-commerce site on virtual machines. Here's what that might look like in your test environment running on Azure. The following illustration shows a three-tier architecture running on virtual machines with security features enabled to restrict inbound requests. 

![An illustration showing a three-tier architecture where each tier is running on a separate virtual machine. Each virtual machine is labelled with its IP address and is inside its own virtual network. Each virtual network has a network security group that lists the open ports.](../media/2-test-deployment.png)

Let's break this down.

### What is an Azure region?

A _region_ is an Azure data center within a specific geographic location. East US, West US, and North Europe are examples of regions. You see that the application is running in the East US region.

### What is a virtual network?

A _virtual network_ is a logically isolated network on Azure. Azure virtual networks will be familiar to you if you’ve set up networks on Hyper-V, VMware, or even on other public clouds.

The web, application, and data tiers each have a single VM. Each VM belongs to a virtual network.

Users interact with the web tier directly, so that VM has a public IP address. Users don't interact with the application or data tiers. So these VMs each have a private IP address.

Azure data centers manage the physical hardware for you. You configure virtual networks through software, which enables you to treat a virtual network just like your own network. For example, you can divide a virtual network into subnets to better control how the network assigns IP addresses. You also choose which other networks your virtual network can reach, whether that’s the public internet or other networks in the private IP address space.

### What's a network security group?

A _network security group_, or NSG, allows or denies inbound network traffic to your Azure resources. Think of a network security group as a cloud-level firewall for your network.

For example, notice that the VM in the web tier allows inbound traffic on ports 22 (SSH) and 80 (HTTP). Each network security group here allows traffic from all sources. You can configure a network security group to accept traffic only from known sources, such as IP addresses that you trust.

> [!NOTE]
> Port 22 enables you to connect directly to Linux systems over SSH. Here we show port 22 open for learning purposes. In practice, you might configure VPN access to your virtual network to increase security.

## Summary

Your three-tier application is now running on Azure in the East US region. A _region_ is an Azure data center within a specific geographic location.

Each tier can access services only from a lower tier. The VM running in the web tier has a public IP address because it receives traffic from the internet. The VMs in the lower tiers, the application and data tiers, each have private IP addresses because they don't communicate directly over the internet.

_Virtual networks_ enable you to group and isolate related systems. You define _network security groups_ to control what traffic can flow through a virtual network.

The configuration you saw here is a good start. But when you deploy your e-commerce site to production in the cloud, you'll likely run into the same problems as you did in your on-premises deployment.
