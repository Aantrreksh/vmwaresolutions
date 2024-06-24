---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Red Hat OpenShift 4.7 additional configuration
{: #openshift-runbook-runbook-config-intro}

## vSphere storage for Kubernetes
{: #openshift-runbook-runbook-config-storage-vsphere}

You can use the VMware vSphere® datastores as a location for storing persistent volumes for Kubernetes by using the VMware® Cloud Provider.

Complete the following steps to create a new volume.

1. From the Bastion host, use GOVC to enable the vSphere connection:

    ```bash
    export GOVC_URL='10.208.17.2'
    export GOVC_USERNAME='administrator@vsphere.local'
    export GOVC_PASSWORD='xxx'
    export GOVC_INSECURE=1
    export GOVC_NETWORK='SDDC-DPortGroup-Mgmt'
    export GOVC_DATASTORE='vsanDatastore'
    ```
    {: pre}

2. Create a folder on the specified datastore:

    ```bash
    govc datastore.mkdir ocp-volumes
    ```
    {: pre}

3. Create a persistent volume (*.vmdk*):

    ```bash
    govc datastore.disk.create -size 10G ocp-volumes/ocp-pv-001.vmdk
    ```
    {: pre}

4. Use the CLI to log in to your Kubernetes environment:

    ```bash
    export KUBECONFIG=/opt/ocpinstall/auth/kubeconfig
    oc login
    ```
    {: pre}

5. Create a persistent volume in Kubernetes for the recently created *.vmdk*. Replace volumePath with your *.vmdk*. The following example uses *vsphere-volume-pv.yaml*.

    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: ocpvsan001
    spec:
      capacity:
        storage: 10Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      vsphereVolume:
        volumePath: "[ESX_OCP] volumes/ocp-pv-001.vmdk"
        fsType: ext4
      storageClassName: "vsphere-standard"
    ```

    ```bash
    export KUBECONFIG=/opt/ocpinstall/auth/kubeconfig
    kubectl create -f  vsphere-volume-pv.yaml
    ```
    {: pre}

6. Create a Persistent Volume Claim in Kubernetes.

    Replace *volumePath* with your Persistent Volume name. The following example uses *vsphere-volume-pvc.yaml*.
    {: note}

    ```yaml
    apiVersion: "v1"
    kind: "PersistentVolumeClaim"
    metadata:
      name: "pvcvsan001"
    spec:
      accessModes:
        - "ReadWriteOnce"
      resources:
        requests:
          storage: "1Gi"
      storageClassName: "vsphere-standard"
      volumeName: "ocpvsan001"
    ```

    ```bash
    kubectl create -f vsphere-volume-pvc.yaml
    ```
    {: pre}

    The persistent volume claim can now be mapped to the container application.  

## Related links
{: #vcs-openshift-runbook-config-related}

* [{{site.data.keyword.vcf-auto}} and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [System context for vCenter Server and {{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-syscontext)
* [{{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-redhat-arch)
* [{{site.data.keyword.vmwaresolutions_full}} SDDC architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-arch)
* [{{site.data.keyword.cloud_notm}} networking and infrastructure](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-sddc-infra)
* [Storage options on {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-storage)
