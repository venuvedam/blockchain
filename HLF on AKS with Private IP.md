# Introduction

Hyperledger Fabric (HLF) has a couple of interesting deployment methodologies on Azure. While there is an all encompassing managed offering from Microsoft based on the Linux Foundation version of HLF, there is also an ARM template that sets up the ledger on the managed Kubernetes orchestrator on Azure - Azure Kubernetes Service. (AKS henceforth)

At present, the AKS template of HLF sets up the ledger with a public IP so that the network can span across an organization's trust boundaries and have nodes from other orgs participating in it. Most blockchain implementations in production follow this path and are invariably multi-org networks. So it makes sense to have the template expose a public IP by default. 

However, there are cases in which the entire ledger (for valid reasons several though it appears off from a blockchain perspective), is in the control of a single organization and there is no requirement for the ledger to have a public facing IP or DNS. From a security point of view, in such cases, it is imperative that there is no such public access.

Unfortunately, as the template is currently designed, it comes with a public IP. In this blog post, we will discuss how you can use this template on Azure to spin up a HLF network and then move it to a completely private network. 

> Before we go any further, this is just one way of accomplishing the task. There may be several other ways of doing it better. If you are implementing your Hyperledger Fabric network from scratch on Azure using a bespoke deployment strategy, this may not apply to you. The purpose of this post is to help you get to that end state by starting with the pre-baked HLF template that is currently available on Azure Marketplace as a first party offering from Microsoft.

> Here is the link to HLF on AKS template: https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-azure-blockchain.azure-blockchain-hyperledger-fabric-aks-based?tab=Overview 
>
> The documentation/help is available at: https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service 

# Working with Private IP/DNS 

------

To start with, set up a single org HLF network on Azure using the template mentioned above. However, choose "Advanced Networking" option while setting it up. You can use the following settings though you are welcome to use your own settings. This is just an example. Before you ask why we are starting with 10.2.0.0 and not 10.1.0.0 - we are reserving that address space for the application layer - the discussion of which is outside the purview of this post.

Also, to answer the question why we are creating two VNets and two separate AKS clusters one for orderer and the other for peer, that is how the HLF on AKS template is currently setup on Azure Marketplace. It makes sense in a distributed HLF network scenario with multiple organisations joining the network. In such a scenario, orderer and peer most likely will not be in the control of a single organisation. Hence the template spins them up as separate deployments. If you want to use a single AKS cluster in a Vnet to host both orderer and peer nodes, you can still do so by working with HLF container images available on Linux Foundation repository and spinning up the AKS cluster from scratch. This document, however, is about using the existing HLF on AKS template and changing the settings post deployment. 

Also a word of caution: This document should be taken as a guidance artifact only. Please do not implement production networks using this guidance without proper testing and validation for your particular use case. 

## Orderer

```
VNet: 10.2.0.0/16

HLF Subnet: 10.2.0.0/24

Kubernetes Service Address Range - 10.2.1.0/24

Kubernetes DNS Service IP Address - 10.2.1.10

Docker Bridge Address - 10.2.3.100/24
```

## Peer

```
VNet: 10.3.0.0/16

HLF Subnet: 10.3.0.0/24

Kubernetes Service Address Range - 10.3.1.0/24

Kubernetes DNS Service IP Address - 10.3.1.10

Docker Bridge Address - 10.3.3.100/24
```

Once the clusters are created, you can follow the steps outlined below to convert the public IP/DNS of the clusters to private.

## Set up VNet Peering

Orderer and Peer clusters will not be able to talk to each other because of the unavailability of public IP. Hence you need to set up VNet peering between the two VNets. Please following the guidance in the link below to set these up. (It needs to be bi-directional)

> https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal

## AKS Settings

> ```
> Mahesh/Surbhi to fill this section
> ```

## Set up the HLF network and the Application Instance

An unfortunate fallout of this is that you cannot use Azure Cloud Shell anymore to interact with this ledger. You have to setup the client instance on a VM running inside either of these VNets. (Or create a new VNet for the client VM and peer it with the rest.) You can use the same instructions mentioned in  https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service to set this up. 

> Make sure that your NPM version is 6.14.5

Once the application instance is ready, set up the HLF network (By exchanging the orderer and peer information with each other) The instructions are available in the link given above.

## Testing

Now that you have done the setup and converted the clusters to use private IP, you have to test if the cluster is still able to function normally. Use the channel creation and anchor peer setting commands in the instructions above to check if everything is working fine. 

