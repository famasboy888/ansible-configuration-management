# Ansible Day-8

## Using Roles management

Reference for **[Roles](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)**.

Foldder Structure of roles:

```bash
roles
├── base
│   └── tasks
│       └── main.yaml
├── worker
│   ├── files
│   │   └── my_custom_script.sh
│   └── tasks
│       └── main.yaml
└── workstation
    └── tasks
        └── main.yaml
```

```bash
---

- hosts: all
  become: true
  roles:            <== Add roles module
    - base          <== is is according to the folder structure given above

- hosts: master
  become: true
  roles:
    - workstation

- hosts: worker
  become: true
  roles:
    - worker
```

**Run command: And target debian tag**
```bash
ansible-playbook roles_execute.yaml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash

PLAY [all] **********************************************************************
TASK [Gathering Facts] **********************************************************
ok: [192.168.2.243]
ok: [192.168.2.240]

TASK [base : Update and Upgrade repo list and pkgs] *****************************
ok: [192.168.2.243]
changed: [192.168.2.240]

PLAY [master] *******************************************************************

TASK [Gathering Facts] **********************************************************
ok: [192.168.2.243]

TASK [workstation : Installing apache on workstation] ***************************
ok: [192.168.2.243]

PLAY [worker] *******************************************************************

TASK [Gathering Facts] **********************************************************
ok: [192.168.2.240]

TASK [worker : Copy custom script to local bin] *********************************
changed: [192.168.2.240]

PLAY RECAP **********************************************************************
192.168.2.240              : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.2.243              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>
