---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Zerto
{: #vum-zerto}

If you find that a vSphere® ESXi™ host can't enter maintenance mode during remediation, it might be that Zerto is stopping it.

If you updated Zerto after the initial deployment, complete the following steps to resolve the issue:
1. Log in to the Zerto web user interface.
2. Click **Site Settings** on the menu.
3. Click the **Policies** tab and ensure that **Allow Zerto to always enter hosts to maintenance mode during remediation** is selected.
4. Log out of Zerto.

If you do not update Zerto after the initial deployment, complete the instructions at [How to place a host with an associated VRA into maintenance mode](https://www.zerto.com/myzerto/knowledge-base/how-to-place-a-host-with-an-associated-vra-into-maintenance-mode/){: external} to resolve the issue.

## Related links
{: #vum-zerto-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
