# Ansible Day-4

## Run Playbook based on Group/Node

Reference for **[Package Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html)**.

```bash
---

- hosts: master                                         <== This will only execute for master group/node
  become: true
  tasks:

  - name: Install apache and nano package
    package:
      name:
         - "{{ apache_package }}"
      state: latest
      update_cache: true

- hosts: worker                                         <== This will only execute for worker group/node
  become: true
  tasks:

  - name: Install apache and nano package
    package:
      name:
         - "{{ nano_package }}"
      state: latest
      update_cache: true
```

Variables are declared inside **inventory file**.

**ansible_user** are declared inside **inventory file**.

```bash
[master]
192.168.2.243 ansible_user=debian apache_package="apache2"

[worker]
192.168.2.240 ansible_user=ubuntu nano_package="nano"
```

**Run command:**
```bash
ansible-playbook install_apache.yml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
PLAY [master] **********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.243]

TASK [Install apache and nano package] *********************************************************************************
ok: [192.168.2.243]

PLAY [worker] **********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.240]

TASK [Install apache and nano package] *********************************************************************************
ok: [192.168.2.240]

PLAY RECAP *************************************************************************************************************
192.168.2.240              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.2.243              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>







