# Implementing Hyperledger Fabric on AKS with Private IP Configuration

## Introduction

Hyperledger Fabric (HLF) offers multiple deployment options on Azure, including a comprehensive managed service and an ARM template for deployment on Azure Kubernetes Service (AKS). While most production blockchain implementations utilize multi-organization networks requiring public IP access, specific use cases demand completely private network configurations for enhanced security.

The current HLF on AKS template deploys with public IP addresses by default to enable cross-organizational network participation. However, organizations requiring private-only deployments need to implement additional configuration steps to achieve full network isolation.

This guide demonstrates how to deploy the HLF on AKS template and subsequently configure it for private network operation, eliminating all public-facing endpoints while maintaining full functionality.

### Prerequisites and Scope

This guide applies specifically to deployments using the pre-configured HLF template available on Azure Marketplace. Organizations implementing custom Hyperledger Fabric deployments from scratch may require different approaches.

**Template Reference**: [HLF on AKS Template](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-azure-blockchain.azure-blockchain-hyperledger-fabric-aks-based?tab=Overview)

**Documentation**: [Hyperledger Fabric Consortium on AKS](https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service)

## Private Network Configuration

### Initial Deployment

Deploy a single-organization HLF network using the Azure template with "Advanced Networking" configuration. The following network settings provide a foundation for private deployment:

**Architecture Overview**: The template creates separate VNets and AKS clusters for orderer and peer nodes, reflecting the distributed nature of multi-organization networks. This separation maintains security boundaries even in single-organization deployments.

> **Note**: Address space 10.1.0.0/16 is reserved for application layer components not covered in this guide.

### Network Configuration

#### Orderer Network

```
VNet: 10.2.0.0/16

HLF Subnet: 10.2.0.0/24

Kubernetes Service Address Range - 10.2.1.0/24

Kubernetes DNS Service IP Address - 10.2.1.10

Docker Bridge Address - 10.2.3.100/24
```

#### Peer Network

```
VNet: 10.3.0.0/16

HLF Subnet: 10.3.0.0/24

Kubernetes Service Address Range - 10.3.1.0/24

Kubernetes DNS Service IP Address - 10.3.1.10

Docker Bridge Address - 10.3.3.100/24
```

### VNet Peering Configuration

Establish bidirectional VNet peering between orderer and peer networks to enable communication in the absence of public IP addresses.

**Reference**: [Connect Virtual Networks with VNet Peering](https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal)

### AKS Private IP Configuration

#### Current Template Components

The template deploys the following public-facing components:

- Ingress controller with host entries mapped to Azure Public DNS Zone
- Nginx service utilizing public IP addresses
- TLS termination service with public IP mapping
- DNS records (A and TXT) configured in Azure Public DNS Zone

#### Required Modifications

Convert these components to use private IP addresses:

1. **Nginx Service**: Add annotation `service.beta.kubernetes.io/azure-load-balancer-internal: true` to force Azure Internal Load Balancer usage
2. **DNS Updates**: Allow ExternalDNS controller to automatically update Azure Public Zone settings, or manually update DNS records to reference private IP addresses
3. **TLS Service**: Apply identical modifications to TLS service configuration
 
### Client Application Setup

Private network configuration requires establishing client connectivity within the VNet infrastructure. Azure Cloud Shell access is no longer available for private networks.

**Setup Requirements**:
- Deploy client VM within existing VNets or create dedicated VNet with peering
- Ensure Node.js NPM version 6.14.5 compatibility
- Follow standard HLF network setup procedures for orderer-peer communication

**Reference**: [HLF Consortium Setup Guide](https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service)

### Network Validation

Verify private network functionality using standard HLF operations:
- Channel creation commands
- Anchor peer configuration
- Transaction processing validation

### Important Considerations

> **Production Deployment Warning**: This guidance provides implementation patterns for private HLF networks. Conduct thorough testing and validation for specific production use cases before deployment.

## Additional Resources

- [Hyperledger Fabric Consortium on Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/blockchain/templates/hyperledger-fabric-consortium-azure-kubernetes-service)
- [Create an Ingress Controller in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/ingress-basic)
- [Secure Access to API Server Using Authorized IP Address Ranges in AKS](https://docs.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges)
- [AKS HTTP Application Routing Add-on](https://docs.microsoft.com/en-us/azure/aks/http-application-routing)
- [Additional Customizations via Kubernetes Annotations](https://docs.microsoft.com/en-us/azure/aks/load-balancer-standard#additional-customizations-via-kubernetes-annotations)
- [Setting up ExternalDNS for Services on Azure](https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/azure.md)