# Ansible Day-3

## Refactoring Ansible Playbook

Referenche for **[Package Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html)**.

```bash
---

- hosts: all
  become: true
  tasks:

  - name: Install apache and nano package
    package:                                     <== Use package module to auto detect OS distro
      name:                                      <== Add multiple packages to be installed. Align under **name:** and add dash.
         - "{{ apache_package }}"                <== Use of variables
         - "{{ nano_package }}"
      state: latest
      update_cache: true                         <== you can add apt update within single play or bloack 
```

Variables are declared inside **inventory file**.

```bash
192.168.2.243 apache_package="apache2" nano_package="nano"
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

TASK [Install apache2 package] *****************************************************************************************
ok: [192.168.2.243]

PLAY RECAP *************************************************************************************************************
192.168.2.243              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>







