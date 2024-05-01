---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-03"

keywords: cyber recovery, IBM Cloud cyber recovery, cyber recovery network interface, network interface cyber recovery, cyber recovery order instance, order cyber recovery, cyber recovery instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Network interface
{: #cr_orderinginstance-net-interface}

You must specify the following network interface settings when you order {{site.data.keyword.cr}}.

## Hostname prefix
{: #cr_orderinginstance-net-interface-hostname-prefix}

The hostname prefix must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.
* The maximum length of the hostname prefix is 10 characters.

The hostname prefix applies to all hosts in the instance.
{: note}

## Domain name
{: #cr_orderinginstance-net-interface-domain-name}

The domain name must meet the following requirements:
* The domain name must consist of three or more strings that are separated by a period (.) with a maximum of 50 characters.
* The first string (NetBIOS name) must start with a lowercase alphabetic character and end with a lowercase alphabetic or numeric character. It must not exceed 15 characters.
* All strings, except for the last one, can contain only lowercase alphabetic, numeric, and hyphen (-) characters.
* No consecutive hyphens are allowed.
* The last string can contain only lowercase alphabetic characters.
* The length of the last string must be in the range 2 - 24 characters.

The maximum length of the Fully Qualified Domain Name (FQDN) for hosts and virtual machines (VMs) is 63 characters. Domain names must accommodate for this maximum length.
{: note}

## DNS configuration
{: #cr_orderinginstance-net-interface-dns-config}

Select the DNS configuration for your instance:

* **Single public Windows® VSI for Active Directory™/DNS** - A single Microsoft® Windows Server VSI for Microsoft Active Directory (AD) is deployed and can be looked up. The VSI functions as the DNS for the instance where the hosts and VMs are registered.
* **Two highly available dedicated Windows server VMs on the management cluster** - Two Microsoft Windows® VMs are deployed, helping enhance security and robustness.

You must provide two Microsoft Windows Server 2019 Standard edition licenses if you configure your instance to use the two Microsoft Windows VMs.
{: important}

Each license can be assigned only to one single physical server and covers up to two physical processors. One Standard edition license can run two virtualized Microsoft Windows VMs per 2-processor server. Therefore, two licenses are required since two Microsoft Windows VMs are deployed in two different hosts.

You have 30 days to activate the VMs.

For more information about ordering Windows Server 2019 licenses, see [Get started with Windows Server 2019](https://learn.microsoft.com/en-us/windows-server/get-started/get-started-with-windows-server){: external}.

## Configure hostnames individually
{: #cr_orderinginstance-net-interface-network-diagram}

You can customize the hostnames prefix individually by toggling the switch on.

The hostnames prefix must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.

## Related links
{: #cr_orderinginstance-net-interface-related-links}

* [Procedure to order {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-order-procedure)
