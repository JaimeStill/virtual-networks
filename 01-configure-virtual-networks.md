# [Configure Virtual Networks](https://learn.microsoft.com/en-us/training/modules/configure-virtual-networks/)

Virtual networks are a fundamental component of private networks that enable resources to communicate securely. Communication can happen between resources, over the internet, and with on-premises networks.

## Things to Know About Azure Virtual Networks

* An Azure virtual network is a logical isolation of the Azure cloud that's dedicated to your subscription.

* You can use virtual networks to provision and manage virtual private networks (VPNs) in Azure.

* Each virtual network has its own Classless Inter-Domain Routing (CIDR) block and can be linked to other virtual networks and on-premises networks.

* You can link virtual networks with on-premises IT infrastructure to create hybrid or cross-premises solutions, when the CIDR blocks of the connecting networks don't overlap.

* You control the DNS server settings for virtual networks, and segmentation of the virtual network into subnets.

## Things to Consider When Using Virtual Networks

Virtual networks can be used in many ways. As you think about the configuration plan for your virtual networks and subnets, consider the following scenarios:

Scenario | Description
---------|------------
Create a dedicated private cloud-only virtual network | Sometimes you don't require a cross-premises configuraiton for your solution. When you create a virtual network, your services and virtual machines within your virtual network can communicate directly and securely with each other in the cluod. You can still configure endpoint connections for the virtual machines and services that require internet communication, as part of your solution.
Securely extend your data center with virtual networks | You can build traditional site-to-site VPNs to securely scale your datacenter capacity. Site-to-site VPNs use IPSEC to provide a secure connection between your corporate VPN gateway and Azure.
Enable hybrid cloud scenarios | Virtual networks give you the flexibility to support a range of hybrid cloud scenarios. You can securely connecto cloud-based applications to any type of on-premises system, such as mainframes and Unix systems.

## Things to Know About Subnets

Subnets provide a way for you to implement logical divisions within your virtual network. Your network can be segmented into subnets to help improve security, increase performance, and make it easier to manage.

There are certain conditions for the IP addresses in a virtual network when you apply segmentation with subnets:

* Each subnet contains a range of IP addresses that fall within the virtual network address space.

* The address range for a subnet must be unique within the address space for the virtual network.

* The range for one subnet can't overlap with the other subnet IP address ranges in the same virtual network.

* The IP address space for a subnet must be specified using CIDR notation.

* You can segment a virtual network into one or more subnets in the Azure portal.

* For each subnet, Azure reserves five IP addresses. The first four addresses and the last address are reserved. Given the IP address range of `192.168.1.0/24`:

    Reserved address | Reason
    -----------------|-------
    `192.168.1.0` | This value identifies the virtual network address.
    `192.168.1.1` | Azure configures this address as the default gateway.
    `192.168.1.2` *and* `192.168.1.3` | Azure maps these Azure DNS IP addresses to the virtual network space.
    `192.168.1.255` | This value supplies the virtual network broadcast address.

## Things to Consider When Using Subnets

Wheny ou plan for adding subnet segments within your virtual network, there are several factors to consider:

* **Consider service requirements.** Each service directly deployed into a virtaul network has specific requirements for routing and the types of traffic that must be allowed into and out of associated subnets. A service might require or create their own subnet. There must be enough unallocated space to meet the service requirements. Suppose you connect a virtual network to an on-premises network by using Azure VPN Gateway. The virtual network must have a dedicated subnet for the gateway.

* **Consider network virtual appliances.** Azure routes network traffic between all subnets in a virtual network, by default. You can override Azure's default routing to prevent Azure routing between subnets. You can also override the default to route traffic between subnets through a network virtual appliance. If you require traffic between resoruces in the same virtual network to flow through a network virtual appliance, deploy the resources to different subnets.

* **Consider service endpoints.** You can limit access to Azure resoruces like an Azure storage account or Azure SQL database to specific subnets with a virtual network service endpoint. You can also deny access ot the resources from the internet. You might create multiple subnets, and then enable a service endpoint for some subnets, but not others. 

* **Consider network security groups.** You can associate zero or one network security group to each subnet in a virtual network. You can associate the same or a different network security group to each subnet. Each network security group contains rules that allow or deny traffic to and from sources and destinations.

* **Consider private links.** Azure Private Link provides private connectivity from a virtual network to Azure platform as as service (PaaS), customer-owned, or Microsoft partner services. Private Link simplifies the network architecture and secures the connection between endpoints in Azure. The service eliminates data exposre to the public internet.

## Things to Know About Creating Virtual Networks

You can create new virtual networks at any time. You can also add virtual networks when you create a virtual machine.

Requirements for creating a virtual network:

* When you create a virtual network, you need to define the IP address space for the network.

* Plan to use an IP address space that's not already in use in your organization.

    * The address space for the network can be either on-premises or in the cloud, but not both.

    * You can't redefine the IP address space for the network after it's created. If you plan your address space for cloud-only virtual networks, you might later decide to connect an on-premises site.

* To create a virtual network, you need to define at least one subnet.

    * Each subnet contains a range of IP addresses that fall within the virtual network address space.

    * The address range for each subnet must be unique within the address space for the virtual network.

    * The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.

* You can create a virtual network in the Azure portal. Provide the Azure subscription, resource group, virtual network name, and service region for the network.

## Plan IP Addressing

You can assign IP addresses to Azure resources to communicate with other Azure resources, your on-premises network, and the internet. There are two types of Azure IP addresses: *private* and *public*.

**Private IP addresses** enable communication with an Azure virtual network and your on-premises network. You create a private IP address for your resource when you use a VPN gateway or Azure ExpressRoute circuit to extend your network to Azure.

**Pubilc IP addresses* allow your resource to communicate with the internet. You can create a public IP address to connect with public-facing services.

## Things to Know About IP Addresses

* IP Addresses can be statically or dynamically assigned.

* You can separate dynamically and statically assigned IP resources into different subnets.

* Static IP addresses don't change and are best for certain situations, such as:

    * DNS name resolution, where a chnage in the IP address requiers updating host records.

    * IP address-based security models that require apps or services to have a static IP address.

    * TLS/SSL certificates linked to an IP address.

    * Firewall rules that allow or deny traffic by using IP address ranges.

    * Role-based virtual machines such as Domain Controllers and DNS servers.

## Things to Consider When Creating a Public IP Address

To create a public IP address, configure the following settings:

* **IP Version:** Select to create an **IPv4** or **IPv6** address, or **Both** addresses. The **Both** option creates two public IP addresses: an IPv4 and an IPv6 address.

* **SKU:** Select the SKU for the public IP address, including **Basic** or **Standard**. The value must match the SKU of the Azure load balancer with which the address is used.

* **Name:** Enter a name to identify the IP address. The name must be unique wihtin the resource group you select.

* **IP address assignment:** Identify the type fo IP address assignment to use.

    * **Dynamic** addresses are assigned after a public IP address is associated to an Azure resource and is started for the first time. Dynamic addresses can change if a resource such as a virtual machine is stopped (deallocated) and then restarted through Azure. The address remains the same if a virtual machine is rebooted or stopped from wtihin the guest OS. When a public IP address resources is removed from a resource, the dynamic address is released.

    * **Static** addresses are assigned when a public IP address is created. Static addresses aren't released until a public IP address resource is deleted. If the address isn't associated to a resource, you can change the assignment method after the address is created. If the address is associated to a resoruce, you might not be able to change the assignment method.

> If you select IPv6 for the IP version, the assignment method must be **Dynamic** for the Basic SKU. Standard SKU addresses are **Static** for both IPv4 and IPv6 addresses.

## Things to Consider When Associating Public IP Addresses

A public IP address resource can be associated with virtual machine network interfaces, internet-facing load balancers, VPN gateways, and application gateways. You can associate your resources with both dynamic and static public IP addresses.

Resoruce | Public IP address association | Dynamic IP address | Static IP address
---------|-------------------------------|--------------------|------------------
Virtual Machine | Nic | Yes | Yes
Load Balancer | Front-end Configuration | Yes | Yes
VPN Gateway | VPN Gateway IP Configuration | Yes | Yes*
Application Gateway | Front-end Configuration | Yes | Yes*

> \* Static IP addresses are available on certain SKUs only.

When you create a public IP address, you select the Basic or Standard SKU. Your SKU choice affetcs the IP assignment method, security, available resources, and redundancy options.

Feature | Basic SKU | Standard SKU
--------|-----------|-------------
IP assignment | Static or Dynamic | Static
Security | Open by default | Secure by default, closed to inbound traffic
Resources | Network interfaces, VPN gateways, Application gateways, and internet-facing load balancers | Network interfaces or public standard load balancers
Redundancy | Not zone redundant | Zone redundant by default

## Things to Consider When Associating Private IP Addresses

A private IP address resoruce can be associated with virtual machine network interfaces, internal load balancers, and application gateways. Azure can provide an IP address (dynamic assignment) or you can assign the IP address (static assignment).

Resource | Private IP association | Dynamic IP address | Static IP address
---------|------------------------|--------------------|------------------
Virtual machine | NIC | Yes | Yes
Internal load balancer | Front-end configuration | Yes | Yes
Application gateway | Front-end configuration | Yes | Yes

A private IP address is allocated from the address range of the virtual network subnet that a resource is deployed in. There are two options: dyanmic and static.

* **Dynamic:** Azure assigns the next available unassigned or unreserved IP address in the subnet's address range. Dynamic assignment is the default allocation method.

    Suppose addresses `10.0.0.4` through `10.0.0.9` are already assigned to other resources. In this case, Azure assigns the address `10.0.0.10` to a new resource.

* **Static:** You select and assign any unassigned or unreserved IP address in the subnet's address range.

    Suppose a subnet's address range is `10.0.0.0/16` and addresses `10.0.0.4` through `10.0.0.9` are already assigned to other resources. In this scenario, you can assign any address between `10.0.0.10` and `10.0.255.254`.