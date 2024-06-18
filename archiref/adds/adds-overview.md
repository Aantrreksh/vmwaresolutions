---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Active Directory overview
{: #adds-overview}

Active Directory™ (AD) Domain Services use DNS name resolution services to locate domain controllers and for the domain controllers that host the directory service to communicate with each other. AD has a logical hierarchical containment structure, where the top-level container is the forest. Within forests are domains, and within domains are organizational units (OUs). This logical model is independent of the physical aspects of the deployment.

## Active Directory terminology
{: #adds-overview-ad}

AD uses the following terminology:

* Forest - A collection of one or more domains that share a common logical structure, directory schema, directory configuration, and global catalog. Domains in the same forest are automatically linked with two-way, transitive trust relationships.
* Domain - A domain is a partition in a forest. Partitioning data enables organizations to replicate data only to where it is needed. In this way, the directory can scale globally over a network that has a limited available bandwidth. The area of a network covered by one single authentication database.
* Schema - A set of rules that define the classes of objects and the attributes that are contained in the directory, the constraints and limits on instances of these objects, and the format of their names.
* Domain controller - Domain controllers provide the physical storage for the Active Directory Domain Services database, in addition to providing the services and data that allows enterprises to effectively manage their servers, workstations, users, and applications. Make domain controllers secure to avoid compromising your Active Directory data.
* Root domain - The root domain contains the Enterprise Admins and Schema Admins groups. These service administrator groups are used to manage forest-level operations such as the addition and removal of domains and the implementation of changes to the schema.
* Parent domain - Several domains can be linked together to form a tree structure. In the hierarchy, the highest level domain is known as the parent domain, and has one or more child domains that are linked to it.
* Child domains - These domains link to a parent domain and inherit the address space of the parent, so the child is a subdomain. A child to one domain can also be the parent to other domains. A child domain name always includes the complete parent domain name. The child and parent domains share a two-way transitive trust.
* Global catalog - A global catalog server is a domain controller that stores partial copies of all Active Directory objects in the forest. It stores a complete copy of all objects in the directory of the domain and a partial copy of all objects of all other forest domains. Users and administrators can find directory information regardless of which domain in the directory contains the data. It is replicated to every domain controller that is a member of that forest.
* AD Sites - In AD, a site represents a physical or logical entity that is defined on the domain controller. Each site is associated with a domain. Each site also has IP definitions of what IP addresses or ranges belong to that site. Domain controllers use site information to inform AD clients about domain controllers present within the closest site to the client.
* Site Links - Site links are used to establish links between AD sites. By configuring the site link properties such as schedule, replication cost, and interval, inter-site replication can be managed.
* Trust - A trust relationship is a logical relationship that is established between domains to allow authentication and authorization to shared resources. The authentication process verifies the identity of the user, and the authorization process determines what the user is allowed to do on a computer system or network.
* Directory - AD uses a structured data store as the basis for a logical, hierarchical organization of directory information. This data store, also known as the directory, contains information about AD objects. These objects typically include shared resources such as servers, volumes, printers, and the network user and computer accounts.
* Replication - A service that distributes directory data across a network. All domain controllers in a domain participate in replication and contain a complete copy of all directory information for their domain. Any change to directory data is replicated to all domain controllers in the domain.
* Organizational units - OUs can be used to form a hierarchy of containers within a domain. OUs are used to group objects for administrative purposes such as the application of Group Policy or delegation of authority. Control (over an OU and the objects within it) is determined by the access control lists (ACLs) on the OU and on the objects in the OU. To facilitate the management of large numbers of objects, Active Directory Domain Services support the concept of delegation of authority. By using delegation, owners can transfer full or limited administrative control over objects to other users or groups. Delegation is important because it helps to distribute the management of large numbers of objects across a number of people who are trusted to perform management tasks.
* Functional levels - Functional levels determine the available Active Directory Domain Services domain or forest capabilities and the Windows® Server operating systems that you can run on domain controllers in the domain or forest. However, functional levels do not affect which operating systems you can run on workstations and member servers that are joined to the domain or forest.

## Domain models
{: #adds-overview-models}

Review the typical domain models available to a customer when they designate their domains either on-premises or in the {{site.data.keyword.cloud}}.

* Single forest, single domain model.
* Single forest, multiple domains model.
* Multiple forests model.

For more information about forest and domain models, see [Designing the logical structure](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/designing-the-logical-structure).

### Single forest, single domain model
{: #adds-overview-models-sfsd}

The single forest, single domain model is the easiest to administer and maintain. The design consists of a forest that contains a single domain. As it is the only domain, it is the forest root domain, and it contains all of the user and group accounts in the forest and the resource objects. For some enterprises, this model is all that is required. However, more complex enterprises can't use this model.

### Single forest, multiple domains model
{: #adds-overview-models-sfmd}

The single forest, multiple domains model is used by larger enterprises where the forest includes many users that are either distributed across different geographic locations or different business units. If each location has its own domain, then replication traffic between locations is reduced. Ease of management is often the use case for domains that are used for different business units. This domain model consists of a forest root domain and one or more regional domains. Often, the forest root domain is restricted to just the Enterprise Admins and Schema Admins groups. These groups are used to manage forest-level operations such as the addition and removal of domains and the implementation of changes to the schema.

Creating a multiple domain model design involves identifying what domain is the forest root domain and determining the number of extra domains that are required to meet your replication requirements. These domains can be parent or child domains, depending on how the domain structure needs to reflect the organizational structure. Typically, it's better to have as few domains as possible to manage. To reduce complexity, the enterprise needs to balance complexity with the separation of resources into different domains and subdomains, which has security benefits.

### Multiple forest models
{: #adds-overview-models-mf}

If the enterprise includes groups that require data isolation or service isolation from other groups in the enterprise, then the multiple forest model can be used to create a separate forest for these groups. Domains do not provide data isolation or service isolation. The forest service administrators have full access to all resources in the forest. This access cannot be prevented, so if you have resources that this group must not have access to, then these resources need to be placed in a different forest.

The multiple forest model is also seen where enterprises have merged, and the two enterprises have two different Active Directory Domain Services structures.

Review the following three forest models.

* Organizational forest model – In this model, user accounts and resources are contained in both forests but managed independently. This model can provide autonomy and isolation, if the forest is configured to prevent access to anyone outside the forest. If users in an organizational forest need to access resources in other forests, or the reverse, trust relationships can be established between one organizational forest and the other forests.
* Resource forest model – In this model, a separate forest is used to manage resources and these forests do not contain user accounts other than the service administrators. Forest trusts are established so that users from other forests can access the resources that are contained in the resource forest. This model provides service isolation.
* Restricted access forest model – In this model, a separate forest is created to contain user accounts and resources that must be isolated from the rest of the enterprise. Users from one forest cannot be granted access to the other forest as no trust exists between the forests. This model is often adopted by service providers who can provide infrastructure management services, for example. In this model, if users need access to resources in both forests, users have an account in one forest and a separate user account in the other forest. This model provides data isolation. The restricted access forest model is created when you provision a {{site.data.keyword.vmwaresolutions_short}} vCenter Server instance.

## Related links
{: #adds-overview-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Getting started with VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-getting-started)
* [More limitations and considerations - Windows automatic installation of updates](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_limitations#trbl_limitations-windows-update)
