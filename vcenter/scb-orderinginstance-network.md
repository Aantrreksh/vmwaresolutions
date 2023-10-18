---

copyright:

  years:  2021, 2023

lastupdated: "2023-08-29"

keywords: order Security and Compliance Readiness Bundle, order scb instances, order vcs scb
subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Network interface settings
{: #scb-orderinginstance-network-interface}

New deployments of Security and Compliance Readiness Bundle instances are no longer supported. You can still add or delete clusters, add or delete VMware ESXi™ servers or NFS storage, and add or remove services for existing instances. You can also view and delete your Security and Compliance Readiness Bundle instances.
{: deprecated}

You must specify the following network interface settings.

## Hostname prefix
{: #scb-orderinginstance-network-interface-host-name-prefix}

The hostname prefix must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.
* The maximum length of the hostname prefix is 10 characters.

The hostname prefix applies to all clusters in the instance.

## Domain name
{: #scb-orderinginstance-network-interface-domain-name}

The root domain name must meet the following requirements:
* The domain name must consist of three or more strings that are separated by a period (.) with a maximum of 50 characters.
* The first string (NetBIOS name) must start with a lowercase alphabetic character and end with a lowercase alphabetic or numeric character. It must not exceed 15 characters.
* All strings, except for the last one, can contain only lowercase alphabetic, numeric, and hyphen (-) characters.
* No consecutive hyphens are allowed.
* The last string can contain only lowercase alphabetic characters.
* The length of the last string must be in the range 2 - 24 characters.

The maximum length of the Fully Qualified Domain Name (FQDN) for hosts and VMs is 63 characters. Domain names must accommodate for this maximum length.
{: note}

## Deployment type
{: #scb-orderinginstance-network-interface-deploy-type}

Two highly available dedicated Windows® server VMs are deployed on the management cluster.
