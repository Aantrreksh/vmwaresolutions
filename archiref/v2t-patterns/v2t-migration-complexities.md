---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-13"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Assess migration complexity
{: #v2t-complexity}

In this step of the process, you can check the source NSX-V environment and use a number of parameters to categorize the migration project. The possible three complexity categories are Low, Medium, or High.

The following diagram depicts the parameters and shows how the values of these parameters map to the complexity assessment.

![Complexity categories](../../images/v2t-diagrams-criteria.svg "Complexity categories"){: caption="Complexity categories" caption-side="bottom"}

You can use the following assessment approach:

1. For each parameter, review your source NSX-V environment and select a complexity classification.
2. Work through all the parameters.
3. At the end of the process, see which complexity column most of your parameter complexity classifications are aligned with:
   * If all are aligned with Low complexity, then the migration complexity is Low. In this case, go to step 5.
   * If most are aligned with Medium complexity but the minority is High, then the migration complexity at this stage is Medium. Go to step 4.
4. For those parameters that are not aligned in one column completely, review them and consider the impact on the classification by using the guidance on key parameters in the following sections. For instance, a key parameter might tip the assessment into a High complexity.

The assessment is complete.

Depending on the source environment complexity and the skills, experience and time commitments of your team, you might want to engage professional services. This action is done to plan and run the migration for you.
{: note}

## Zone deployment
{: #v2t-complexity-zone}

Your source {{site.data.keyword.vcf-auto}} instance with NSX-V environment is in one of the following deployment patterns:

* Simple - one single zone, with all VMware ESXi™ hosts deployed in one data center.
* Medium - two or more single zones, often used as production in one zone and development or DR in another zone.
* Medium - two or more single zones in a site deployment with no cross vCenter NSX-V.
* High - two or more single zones in a multisite deployment with cross vCenter NSX-V.
* High - multizone, with ESXi hosts deployed in multiple data centers.

{{site.data.keyword.vmwaresolutions_full}} offers standard deployment models, and multisite deployments require manual customization to build the wanted network topology. 

This is a key parameter and defines the classification of the migration project and the required VMware NSX-T™ skills.

## Size
{: #v2t-complexity-size}

The size parameter is based on the number of virtual machines and clusters. This parameter defines the scale and the length of the migration project. Larger environments are more complex, but not always.

This is not a key parameter. Therefore, if you have more than 1000 VMs, it does not classify the migration project as High complexity.

## vCenter deployment
{: #v2t-complexity-vc}

Is your vCenter deployed as independent or is it using the vCenter HA pattern? vCenter HA is not deployed as part of automation. If you want to deploy it, you must do the customization post deployment manually.

This is not a key parameter. However, it is related to the zone deployment category. 

## ADDNS customization
{: #v2t-complexity-addns}

The primary use of {{site.data.keyword.vcf-auto}} instance ADDNS is to provide Active Directory™ and Domain Name Services to the infrastructure only. If you don't customize ADDNS, then the classification is Simple.

If you customize the service, such as by integrating it with your own AD or by using it for AD or DNS of workloads, you must complete extra tasks. This action is done to migrate the customization to the target instance's new ADDNS.

This is not a key parameter. However, it gives guidance on where more project tasks and skills are required.

## Overlay and underlay network customization
{: #v2t-complexity-network}

If you customize your underlay or overlay networks, review the customizations and the following areas:

* Additional {{site.data.keyword.cloud_notm}} public or private VLANs.
* Additional portable subnets.
* Consumption of IP addressing from reserved subnets.
* Multitenant overlay deployments.
* Multiple GRE or IPsec tunnels.
* Use of hardware VTEPs - The classification becomes High complexity.

Due to the architectural differences between NSX-V and NSX-T, these aspects might require advanced configuration skills to build the wanted network topology. 

This is a key parameter and defines the classification of the source environment. 

## Layer 2 stretched overlay
{: #v2t-complexity-l2}

If you use NSX-V to stretch layer 2 networks across data centers, then the classification is Medium and High. Due to the architectural differences between NSX-V and NSX-T, these aspects might require advanced configuration skills to build the wanted network topology. 

This is not a key parameter. However, it is related to the zone deployment category and adds more weighting to the complexity. 

## Gateway firewall
{: #v2t-complexity-gwfw}

Does your source environment include gateway firewalls such as FortiGate®, vRAs, or Juniper® vSRX?

Due to the architectural differences between NSX-V and NSX-T, these aspects might require advanced configuration skills to build the wanted network topology. In some cases, gateway firewalls might be rebuilt with new IP addresses. For example, when the new deployment is in a new {{site.data.keyword.cloud_notm}} data center or POD. This action requires skills and work effort to reconfigure the related firewalls.

This is not a key parameter. However, it gives guidance on where more project tasks and skills are required.

## Distributed firewall
{: #v2t-complexity-dfw}

If you use the NSX-V distributed firewalling feature, the configurations must be migrated to the NSX-T environment. The number and complexity of these rules impact the migration. Depending on the complexity of the rules, some of them can be migrated easily. However, if the rules use vCenter tagging, then they cannot be migrated as-is, as this feature doesn't exist in NSX-T. Consider the usage of a third-party tool for a large number or complex use of distributed firewall.

This is a key parameter and also gives guidance on where more project tasks, tools, and skills are required. 

## Load balancing
{: #v2t-complexity-lb}

The use of load-balancers number and the complexity of the rules impact the migration of the VMs. Due to the architectural differences between NSX-V and NSX-T, these aspects might require advanced configuration skills to build the wanted load-balancing solution.

This is not a key parameter. However, it gives guidance on where more project tasks and skills are required.

## Additional services
{: #v2t-complexity-services}

The optional vCenter server instance services, such as Veeam or Zerto are linked to your vCenter server instance. By deleting the source {{site.data.keyword.vcf-auto}} instance, these services are deleted, and so are your historical backups. 

You must reconfigure the services or migrate configurations post-deployment. This action is done to match your needs and requirements in the new target NSX-T based {{site.data.keyword.vcf-auto}} instance.

This is not a key parameter. However, it gives you guidance on where additional project tasks and skills are required or if you must take a different approach for the additional services.

## Related links
{: #v2t-complexity-links}

* [{{site.data.keyword.vcf-auto}} single site](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [{{site.data.keyword.vcf-auto}} multisite](/docs/vmwaresolutions?topic=vmwaresolutions-vc_multisite)
* [Regulated workloads - single site](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overview)
* [Ordering services for {{site.data.keyword.vcf-auto}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
