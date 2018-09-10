Securing your network from attacks and unauthorized access is an important part of any architecture. Here, we'll take a look at what network security looks like, how to integrate a layered approach into your architecture, and how Azure can help you provide network security for your environment.

## A layered approach to network security

A common thread throughout this module has been taking a layered approach to security, and this approach is no different at the network layer. It's not enough to just focus on securing the network perimeter, or focusing on the network security between services inside a network. A layered approach provides multiple levels of protection, so that if an attacker gets through one layer, there's further protections in place to limit further attack.

Let's take a look at how Azure can provide the tools for a layered approach to securing your network footprint.

### Internet protection

If we start on the perimeter of the network, we're focused on limiting and eliminating attacks from the internet. A great first place to start is to assess the resources that are internet-facing, and allow only inbound and outbound communication where necessary. Identify all resources that are allowing inbound network traffic of any type, and ensure they are necessary and restricted to only the ports/protocols required. Azure Security Center is a great place to look for this information, because it will identify internet-facing resources that don't have network security groups associated with them, as well as resources that are not secured behind a firewall.

To provide inbound protection at the perimeter, you have a couple of choices:

* Azure Application Gateway is a load balancer that includes a web application firewall that provides protection from common, known vulnerabilities.

* For non-HTTP services or advanced configurations, network virtual appliances (NVAs) can be used. NVAs are similar to hardware firewall appliances.


Any resource exposed to the internet is at risk of being attacked by a denial of service attack. These types of attacks attempt to overwhelm a network resource by sending so many requests that the resource becomes slow or unresponsive. To mitigate these attacks, Azure DDoS protection provides basic protection across all Azure services and enhanced protection for further customization for your resources. Azure DDoS protection blocks attack traffic and forwards the remaining traffic to its intended destination. Within a few minutes of attack detection, you are notified using Azure Monitor metrics.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![DDoS](../media-COPIED-FROM-DESIGNFORSECURITY/ddos.png)

### Virtual network security

Once inside a virtual network (VNet), it's important to limit communication between resources to only what is required.

For communication between virtual machines, network security groups are a critical piece to restrict unnecessary communication. They provide a list of allowed and denied communication to and from network interfaces and subnets, and are fully customizable.

You can completely remove public internet access to your services by restricting access to service endpoints. With service endpoints, Azure service access can be limited to your virtual network.

### Network integration

It's common to have existing network infrastructure that needs to be integrated to provide communication from on-premises networks or to provide improved communication between services in Azure. There are a few key ways to handle this integration and improve the security of your network.

Virtual private network (VPN) connections are a common way of establishing secure communication channels between networks. Connection between Azure Virtual Network and an on-premises VPN device is a great way to provide secure communication between your network and your VNet on Azure.

To provide a dedicated, private connection between your network and Azure, you can use Azure ExpressRoute. ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection facilitated by a connectivity provider. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and Dynamics 365. This improves the security of your on-premises communication by sending this traffic over the private circuit instead of over the internet. You don't need to allow access to these services for your end users over the internet, and youcan send this traffic through appliances for further traffic inspection.

## Summary

A layered approach to network security helps reduce your risk of exposure through network-based attacks. Azure provides several services and capabilities to secure your internet-facing resource, internal resources, and communication between on-premises networks. These features make it possible to create secure solutions on Azure.