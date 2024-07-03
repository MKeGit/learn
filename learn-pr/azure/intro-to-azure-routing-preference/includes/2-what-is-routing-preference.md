As the lead network engineer for the traffic cost-savings project for the Singapore factory, your first step is to understand routing preference and its core features. This overview should help you decide if routing preference in Azure is a good fit for the factory cost-savings project.

Routing preference in Azure allows you to route your traffic through either the Microsoft network or the public internet (ISP network). These options are known as *cold potato routing* and *hot potato routing* respectively. The cost of egress data transfer varies based on your routing choice. You can select your routing preference, either *Microsoft network* or *Internet routing*, when you create a public IP address.

Public IP addresses are associated with resources such as virtual machines, virtual machine scale sets, and internet-facing load balancers. You can also set the routing preference for Azure storage resources such as blobs, files, web, and Azure Data Lake. By default, all Azure services route their traffic through the Microsoft global network. Once a public IP address is created in Azure, its routing preference can't be changed. To change the routing preference of an existing application or service, create a new public IP address with the appropriate routing preference and associate it with the application or service.

## Routing preference - Microsoft network

By default, all Azure services traffic is routed through the Microsoft global network. By routing your traffic through the Microsoft global network, you're utilizing one of the largest networks in the world. The network is equipped with multiple redundant fiber paths to guarantee exceptional reliability and availability. A software-defined WAN controller manages network traffic. The WAN controller ensures that your traffic takes the lowest latency path and provides premium network performance. Ingress and egress traffic stays on the Microsoft global network whenever possible.

:::image type="content" source="../media/route-via-microsoft-global-network.png" alt-text="Diagram of Microsoft network routing preference.":::

## Routing preference - Internet (ISP network)

The *Internet routing* preference minimizes travel on the Microsoft network. The transit ISP network routes the traffic. The Internet routing preference is a cost-optimized option that offers network performance comparable to other cloud providers.

:::image type="content" source="../media/route-via-isp-network.png" alt-text="Diagram of Internet routing preference.":::

## What is routing preference unmetered?

The *routing preference unmetered* service is available for content delivery network (CDN) providers who have their customers' origin content hosted in Azure. This service enables CDN providers to establish a direct peering connection with Microsoft's global network edge routers at various locations. To utilize the benefits of routing preference unmetered, your CDN provider must be enrolled in the program. If your current CDN provider isn't a part of the program, reach out to them for assistance.

:::image type="content" source="../media/unmetered.png" alt-text="Diagram of routing preference unmetered.":::
