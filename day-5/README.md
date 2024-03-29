# Ansible Day-4

## Run Playbook based on Tags

Reference for **[Tags](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_tags.html)**.

```bash
---

- hosts: master
  become: true
  tasks:

  - name: Installing on Debian master
    tags: debian                              <== adding tag to target debian only
    package:
      name:
         - "{{ apache_package }}"
      state: latest
      update_cache: true

- hosts: worker
  become: true
  tasks:

  - name: Installing on Ubuntu worker
    tags: ubuntu                             <== adding tag to target ubuntu only
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

Check List of tags:
```bash
ansible-playbook --list-tags install_apache.yaml
```

```bash
playbook: install_apache.yaml

  play #1 (master): master      TAGS: []
      TASK TAGS: [debian]

  play #2 (worker): worker      TAGS: []
      TASK TAGS: [ubuntu]

```


**Run command: And target debian tag**
```bash
ansible-playbook --tags debian install_apache.yaml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
PLAY [master] **********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.243]

TASK [Installing on Debian master] *************************************************************************************
ok: [192.168.2.243]

PLAY [worker] **********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.240]

PLAY RECAP *************************************************************************************************************
192.168.2.240              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.2.243              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>







