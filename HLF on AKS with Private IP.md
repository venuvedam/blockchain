# Introduction

Hyperledger Fabric (HLF) has a couple of interesting deployment templates on Azure. While there is an all encompassing managed offering from Microsoft based on the Linux Foundation version of HLF, there is also an ARM template that sets up the ledger on the managed Kubernetes orchestrator on Azure - Azure Kubernetes Service. (AKS henceforth)

At present, the AKS template of HLF sets up the ledger with a public IP so that the network can span across an organization's boundary and have nodes from other orgs participating in it. Most blockchain implementations in production follow this path and are invariably multi-org networks. So it makes sense to have the template expose a public IP by default. 

However, there are cases in which the entire ledger (for valid reasons several though it appears off from a blockchain perspective), is in the control of a single organization and there is no requirement for the ledger to have a public facing IP or DNS. From a security point of view, in such cases, it is imperative that there is no such public access.

Unfortunately, as the template is currently designed, it comes with a public IP. In this blog post, we will discuss how you can use this template on Azure to spin up a HLF network and then move it to a completely private network. 

```
Before we go any further, this is just one way of accomplishing the task. There may be several other ways of doing it better. If you are implementing your Hyperledger Fabric network from scratch on Azure using a bespoke deployment strategy, this may not apply to you. The purpose of this post is to help you get to that end state by starting with the pre-baked HLF template that is currently available on Azure Marketplace as a first party offering from Microsoft.
```

Here is the link to HLF on AKS template: https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-azure-blockchain.azure-blockchain-hyperledger-fabric-aks-based?tab=Overview 

The documentation/help is available at: https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service 

# Working with Private IP/DNS 

To start with, set up a single org HLF network on Azure using the template mentioned above. However, choose "Advanced Networking" option while setting it up. You can use the following settings.(You are welcome to use your own settings. This is just an example)

## Orderer

```
VNet: 10.3.0.0/16

HLF Subnet: 10.3.0.0/24

Kubernetes Service Address Range - 10.3.1.0/24

Kubernetes DNS Service IP Address - 10.3.1.10

Docker Bridge Address - 10.3.3.100/24
```

## Peer

```
VNet: 10.2.0.0/16

HLF Subnet: 10.2.0.0/24

Kubernetes Service Address Range - 10.2.1.0/24

Kubernetes DNS Service IP Address - 10.2.1.10

Docker Bridge Address - 10.2.3.100/24
```

