---
title: 7 - Single-Region Virtual WAN with Azure Firewall
weight: 7
---

A full platform landing zone deployment with Virtual WAN network connectivity using Azure Firewall in a single region.

{{< hint type=warning >}}
The single region option is here for completeness, we recommend always having at least 2 regions to support resiliency.
{{< /hint >}}

* Example platform landing zone configuration file: [full-single-region/virtual-wan.tfvars](https://raw.githubusercontent.com/Azure/alz-terraform-accelerator/refs/heads/main/templates/platform_landing_zone/examples/full-single-region/virtual-wan.tfvars)

## Resources

The following resources are deployed by default in this scenario:

### Management

#### Management Groups

- Management Groups
- Policy Definitions
- Policy Set Definitions
- Policy Assignments
- Policy Assignment Role Assignments

#### Management Resources

- Log Analytics Workspace
- Log Analytics Data Collection Rules for AMA
- User Assigned Managed Identity for AMA
- Automation Account

### Connectivity

#### Azure DDOS Protection Plan

- DDOS Protection Plan

#### Azure Virtual WAN

- Virtual WAN
- Virtual Hubs in one region

#### Azure Virtual Networks

- Sidecar Virtual Network
- Sidecar to Virtual Hub peering
- Subnets for Bastion, and Private DNS Resolver in one region

#### Azure Firewall

- Azure Firewall in one region
- Azure Firewall public IP in one region
- Azure Firewall policy in one region

#### Azure Bastion

- Azure Bastion in one region
- Azure Bastion public ip in one region

#### Azure Private DNS

- Azure Private DNS Resolver in one region
- Azure non-regional Private Link Private DNS zones in one region
- Azure regional Private Link Private DNS zones in one region
- Azure Virtual Machine auto-registration Private DNS zone in one region
- Azure Private Link DNS zone virtual network links in one region

#### Azure Virtual Network Gateways

- Azure ExpressRoute Virtual Network Gateway in one region
- Azure VPN Virtual Network Gateway in one region

## Configuration

The following relevant configuration is applied:

### Azure DNS

Private DNS is configured ready for using Private Link and Virtual Machine Auto-registration. Spoke Virtual Networks should use the Azure Firewall IP Address as their DNS configuration.

- Azure Firewall is configured as DNS proxy
- Azure Firewall forwards DNS traffic to the Private DNS resolver
- Azure Private DNS Resolver has an inbound endpoint from the sidecar network
- Azure Private Link DNS zones are linked to the all hub sidecar Virtual Networks
