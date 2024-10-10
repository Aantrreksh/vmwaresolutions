---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# vCenter Single Sign On
{: #adds-sso}

VMware vCenter Single Sign-On (SSO) is an authentication broker and security token exchange infrastructure, which allows VMware vSphere components to communicate with each other through a secure token mechanism and uses the following services:

* Security Token Service (STS)
* SSL for secure traffic
* Authentication of users by using an identity source such as Active Directory™ or OpenLDAP

Review the following vSphere SSO flow.

1. A user logs in to the vSphere Client with a username and password to access vCenter or a vCenter service.
2. The vSphere Client passes the login information to the SSO service, which checks the SAML token of the vSphere Client. If the vSphere Client has a valid token, SSO checks:
   * If the user ID is `@vsphere.local`, then it checks the user against the local SSO domain.
   * If the user ID is `@DOMAIN`, then SSO uses the identity source to check that domain.
3. If authentication is successful SSO returns a token that represents the user to the vSphere Client.
4. The vSphere Client passes the token to vCenter.
5. vCenter checks with SSO that the token is valid and is not expired.
6. The user can view and modify any objects that the user's role has privileges for.

The vSphere SSO domain is used as the initial authentication mechanism and it serves to connect an instance or multiple linked instances to the AD servers in the {{site.data.keyword.vmwaresolutions_full}} infrastructure domain. In the {{site.data.keyword.vmwaresolutions_short}} vCenter Server design, the following SSO configuration is applied:

* The SSO domain of `vsphere.local` is always used.
* The SSO site name equals the `<root_domain>` captured during the ordering process.
* An identity source, the {{site.data.keyword.vmwaresolutions_short}} infrastructure domain `<root_domain>`, is configured.
* The `VSPHERE.LOCAL\Administrator` user is configured as an Administrator role.
* The following groups are configured with Administrator roles:
   * `<root_domain>\ic4v-vCenter`
   * `vsphere.local\Administrators`

After deployment, the `administrator@vsphere.local` user has administrator access to both SSO and vCenter Server. This user can manage identity sources and default domains, specify password policies, and perform other administrative tasks in the `vsphere.local` domain. However, this user is integral to the VMware vSphere® and VMware NSX® infrastructure authentication they are not part of AD but created automatically when vSphere is deployed. As this account is not part of AD, they can be used in situations when AD is not working correctly.

As the customer, you have full access to manage the vSphere SSO users and groups as needed. For more information about changing these policies, see [Managing vCenter Single Sign-On users and groups](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.psc.doc/GUID-31F302A6-D622-4FEC-9007-EE3BA1205AEA.html){: external}.

## Identity sources
{: #adds-sso-identity}

Identity sources are used to attach one or more domains to vCenter SSO. A domain is a repository for users and groups that the vCenter SSO can use for user authentication. vCenter SSO has the following domains that are configured after the vCenter Server instance deployment.

* Local OS - Local operating system users are local to the operating system where the vCenter Single Sign-On server is running. The local operating system identity source exists only in basic vCenter SSO deployments and is not available in deployments with multiple vCenter SSO instances. Only one local operating system identity source is allowed. Shown as local in the vSphere Client.
* vsphere.local – Enables `administrator@vsphere.local` to be authenticated.
* {{site.data.keyword.vmwaresolutions_short}} infrastructure domain – This domain is the <root_domain> configured on the AD DNS server based on the parameters that are collected during the ordering process. This process allows the user `automation@<root_domain>` to be authenticated.

Users can log in to vCenter Server only if they are in a domain that is added as a vCenter SSO identity source. You can add more identity sources to give your AD or LDAP users access if required.

## vSphere SSO configuration
{: #adds-sso-config}

The following sections provide the settings that are configured in vSphere SSO.

### Token trustworthiness
{: #adds-sso-config-token}

| Parameter                            | Value               |
| :----------------------------------- | :------------------ |
| Clock tolerance                      | 600000 milliseconds |
| Maximum token renewal count          | 10                  |
| Maximum token delegation count       | 10                  |
| Maximum bearer token lifetime        | 300 seconds         |
| Maximum holder-of-key token lifetime | 2592000 seconds     |
{: caption="Token trustworthiness" caption-side="bottom"}

### Lockout policy
{: #adds-sso-config-lockout}

For more information about the lockout policy, see [Policy configurations](/docs/vmwaresolutions?topic=vmwaresolutions-vc_compl_info#vc_compl_info-default-policy-config).

### Password policy
{: #adds-sso-config-pwd-policy}

| Parameter | Value  |
| :-------- | :----- |
| Maximum lifetime | Password must be changed every 90 days |
| Restrict reuse | Users cannot reuse any previous five passwords |
| Maximum length | 20 characters |
| Minimum length | 15 characters |
| Character requirements | * At least two alphabetic characters \n * At least one special character \n * At least one uppercase character \n * At least one lowercase character \n * At least one numeric character \n * Identical adjacent characters - 3 |
{: caption="Password policy" caption-side="bottom"}

As the customer, you have full access to tailor these settings as needed to apply your enterprise security policies. For changing these policies, see [Managing vCenter single sign-on policies](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.psc.doc/GUID-43527B09-63BB-44A6-91D3-E3A470904698.html){: external}.

## vSphere ESXi hosts
{: #adds-sso-esxi}

Each vSphere ESXi host has its own `root` account and password. To identify this password, complete the following steps:
1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources** > **vCenter Server** from the left navigation pane.
2. Locate and click the instance.
3. Click the **Infrastructure** tab and click the required cluster.

The vSphere ESXi hosts also join AD so that each system administrator can log in with their own account.

## Related links
{: #adds-sso-related}

* [Common services design](/docs/vmwaresolutions?topic=vmwaresolutions-design_commonservice)
* [Post-deployment considerations for your VMware instance - Active Directory](/docs/vmwaresolutions?topic=vmwaresolutions-solution_considerations#solution_considerations-ad)
