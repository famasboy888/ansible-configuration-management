# Ansible Day-2

## Running Ansible Playbook in worker instance

### Ansible Playbook is written in **YAML file**
```bash
sudo nano install_apache.yml
```

Referenche for **apt module**: [Ref linkn](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html)

```bash
---                                            <== starts with 3 dash lines

- hosts: all                                   <== beginning of statement or block starts with dash and one space. Similar to "all" in basic ansible command.
  become: true                                 <== align "become" to "hosts". This line will enable sudo.
  tasks:                                       <== "tasks" is where you will declare the start of tasks

  - name: Install apache2 package              <== This is the first "play". It is aligned with "tasks". It beginns with dash and one space. It is just giving name in the output.
    apt:                                       <== This is the module. It is aligned to "name". It will install package.
      name: apache2                            <== This is the module. It is aligned to "name". It will install package for "apache2".
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
changed: [192.168.2.243]

PLAY RECAP *************************************************************************************************************
192.168.2.243              : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>


