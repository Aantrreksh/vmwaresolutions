---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Securing the Linux hardened repository server
{: #veeam-cr-sag-lhbrsecure}

This step describes the Ansible® playbook that secures the Linux® hardened backup repository server after it is added to the Veeam® backup infrastructure. The playbook does the following tasks:

* (Optional) [Adds a user](#veeam-cr-sag-lhbrsecure-user) with the name `ansible`.
* [Secures the SSH access](#veeam-cr-sag-lhbrsecure-ssh).

The playbook can be written locally on your laptop by using an editor, such as Visual Studio Code, and transferred to the automation server `\swlib\ansible` directory, or edited locally on the automation server in a text editor, such as `vi` or `nano`.

## Creating the playbook
{: #veeam-cr-sag-lhbrsecure-play}

The playbook `secure_lhbr.yml` starts with the following code:

```text
- hosts: lhbr
  vars:
    vbr_ip: <vbr_ip>
    ansible_ip: <ansible_ip>
```
{: codeblock}

Replace `<vbr_ip>` and `<ansible_ip>` in the previous code snippet with the values that you captured in the earlier steps.

## Adding a user
{: #veeam-cr-sag-lhbrsecure-user}

The task to add an automation user so that the server can be maintained, such as updated, is optional.

Without the automation user, the server has no remote SSH access as the root user is unable to connect through SSH, and the `veeamuser` has no SSH access. Access to the server is possible through the remote console through the IPMI connection.

If you choose this optional task, then you need to change the Ansible inventory file `hosts` to `ansible_user=ansible`.
{: note}

The following code snippet does these actions:

* Adds a user with the name `ansible`.
* Copies the ansible user's public key to the `authorized_hosts` file.
* Allows the ansible user to run a `sudo` command without a password.

```text
  tasks:
    - name: Add the user 'ansible' with a bash shell
      ansible.builtin.user:
        name: ansible
        shell: /bin/bash
        create_home: yes
        state: present
        groups: wheel
        append: yes

    - name: Add ansible public key
      authorized_key:
        user: ansible
        key: "{{ lookup('file', '/home/ansible/.ssh/id_rsa.pub') }}"

    - name: "Allow ansible user to sudo without a password"
      lineinfile:
        dest: "/etc/sudoers"
        state: "present"
        insertafter: "^#includedir /etc/sudoers.d"
        line: "ansible  ALL=(ALL) NOPASSWD: ALL"
```
{: codeblock}

## Securing the SSH access
{: #veeam-cr-sag-lhbrsecure-ssh}

The following code snippet secures the SSH access:

```text
    - name: Allow public key authentication
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^#PubkeyAuthentication yes"
        line: "PubkeyAuthentication yes"
        state: present

    - name: Disallow password authentication
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^PasswordAuthentication"
        line: "PasswordAuthentication no"
        state: present

    - name: Allow ansible access only
      lineinfile:
        dest: /etc/ssh/sshd_config
        line: "AllowUsers ansible@{{ ansible_ip }}"
        state: present

    - name: Disallow root SSH access
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^PermitRootLogin"
        line: "PermitRootLogin no"
        state: present

    - name: Limit idle time to 2 mins
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^#ClientAliveInterval 0"
        line: "ClientAliveInterval 120"
        state: present

    - name: Do not permit empty passwords
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^#PermitEmptyPasswords no"
        line: "PermitEmptyPasswords no"
        state: present

    - name: Disable X11 forwarding
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "^X11Forwarding yes"
        line: "X11Forwarding yes"
        state: present

    - name: Limit max authentication attempts to 3
      lineinfile:
        dest: /etc/ssh/sshd_config
        regexp: "#MaxAuthTries 6"
        line: "MaxAuthTries 3"
        state: present
      notify: Restart ssh

    - name: Restart ssh
      service:
        name: sshd
        state: restarted
```
{: codeblock}

If you are creating the cyber-recovery immutable backup solution architecture, then the tasks are completed. For creating the cyber-recovery isolated recovery environment solution architecture, see [Creating the airgap by using Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-vsrx).

## Related links
{: #veeam-cr-sag-lhbrsecure-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
