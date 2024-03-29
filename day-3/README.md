# Ansible Day-3

## Adding "when" conditions

Referenche for **[Conditionals](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html#conditionals-based-on-ansible-facts)**.

```bash
---

- hosts: all
  become: true
  tasks:

  - name: apt update repository index
    apt:
      update_cache: true
    when: ansible_distribution in ['Debian'] and ansible_distribution_version == "12"    <== adding conditions

  - name: Install apache2 package
    apt:
      name: apache2
      state: latest
```
**Run command:**
```bash
ansible-playbook install_apache.yml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
PLAY [all] *************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.243]

TASK [apt update repository index] *************************************************************************************
changed: [192.168.2.243]

TASK [Install apache2 package] *****************************************************************************************
changed: [192.168.2.243]

PLAY RECAP *************************************************************************************************************
192.168.2.243              : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>







