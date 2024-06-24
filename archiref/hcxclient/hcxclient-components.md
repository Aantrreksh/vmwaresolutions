---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Glossary of HCX components and terms
{: #hcxclient-components}

VMware HCX™ consists of a cloud side (target or virtual data center environment) and one or more clients (source). An instance of HCX must be deployed per vCenter, even if the vCenters where HCX is deployed are linked in the same SSO domain on the client or cloud side. Configurations that are supported by HCX are, one-to-one, one-to-many, many-to-one, and many-to-many.

## Target side and client side
{: #hcxclient-components-cloud-client-side}

HCX has the concept of cloud side (target or virtual data center environment) and client side (source).
* Target side - HCX Cloud is pre-deployed and configured with the network and compute profiles ready for service mesh creation.  
* Client side - Any vSphere instances that meet the prerequisites for installation and operation. The client side of HCX is the primary that controls the cloud side secondary instance through its vCenter web client user interface snap-in.

## HCX Managers
{: #hcxclient-components-hcx-manager}

* The cloud side - HCX Cloud is configured to listen for incoming client-side registration, management, and control traffic.
* The client-side - HCX Connector is a client-side specific OVA image file that provides the user interface functions for managing and operating HCX. The client-side HCX Manager is responsible for registration with the HCX Cloud and creating a management plane between the client and cloud side. Furthermore, it is responsible for deploying a service mesh on the client side and instructing the cloud side to do the same.

## Service Mesh Components
{: #hcxclient-components-fleet}

HCX Service Mesh components are responsible for creating the data and control planes between client and cloud side. Deployed as virtual machines (VMs) in mirrored pairs, the service mesh consists of the following components:
* Interconnect Appliance (HCX-IX) - The interconnect appliance creates encrypted tunnels that support vMotion and replication (bulk migration) traffic.
* WAN Optimizer Appliance (HCX-WAN) - HCX includes an optionally deployed Silver Peak™ WAN optimization appliance. It is deployed as a VM appliance. When deployed, the CGW tunnel traffic is redirected to traverse the WAN Optimizer. Since the WAN optimizer significantly decreases traffic across the WAN (typically 3:1 to 6:1 observed) while it increases connection reliability, it is recommended to deploy the WAN optimizer with the CGW. The added benefit of deploying the WAN optimizer is extended to limit the WAN bandwidth used by VM migration traffic. The WAN optimizer management interface is not configured by default.
* Network Extension (HCX-NE) - Provides the Layer 2 network extension capabilities, enabling migrations between the on-premises location and the vSphere environment with the need to reassign IP addresses to the VMs.
* Proxy ESXi host - Whenever the HCX-IX is configured to connect to the cloud-side HCX site, a proxy ESXi host appears in the VMware vCenter® outside of any cluster. This ESXi host has the same management and vMotion IP address as the corresponding HCX-IX appliance. As a result, the vSphere environment at both the client and the cloud side work as if it performs a local vMotion.

This method has the following benefits:
* The management IP ranges on either side might be overlapping with no loss in functions.
* The cloud side has no vSphere visibility into the client side, which makes it more secure.

## HCX user portals
{: #hcxclient-components-hcx-user-portals}

* Client web user interface – The HCX client web portal is the main user interface for HCX. After the client-side HCX Manager is installed, it shows up as a snap-in to the vCenter web user interface. It controls remote cloud HCX registration (site pairing), fleet component deployment, network stretching, and VM migration into and out of the Cloud.
* Cloud-side user interface – The cloud-side HCX user interface is accessible through the public registration URL given for HCX client registration. By default, it uses the cloud-side vCenter Admin credentials `administrator@vsphere.local`. It is typically used for upgrading the installation and modifying some network configuration.

## Related links
{: #hcxclient-components-related}

* [Port access requirements for VMware HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-port-req)
* [Preparing the installation environment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-planning-prep-install)
* [HCX Client deployment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-client-deployment)
* [HCX on-premises Service Mesh](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-mesh-deployment)
* [VMware Hybrid Cloud migrations](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-migrations)
* [Monitoring parameters and components](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-monitoring)
* [HCX troubleshooting](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-troubleshooting)
