# Ansible Day-10

## Using Roles management

Reference for **[host_vars](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)**.

Reference for **[Handlers](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html)**.

Foldder Structure of roles:

```bash
├── ansible.cfg
├── host_vars                                      <== Declare variables here
│   ├── 192.168.2.240.yaml                         <== Make sure to name them according to "inventory file"
│   └── 192.168.2.243.yaml
├── inventory
├── README.md
├── roles
│   ├── base
│   │   └── tasks
│   │       └── main.yaml
│   ├── worker
│   │   ├── files                                  <== You can store files here
│   │   │   └── my_custom_script.sh
│   │   ├── handlers                               <== Use "handlers" folder for notify module. Treat it similar to calling a function if there are changes
│   │   │   └── main.yaml
│   │   └── tasks
│   │       └── main.yaml
│   └── workstation
│       └── tasks
│           └── main.yaml
└── roles_execute.yaml

```

### roles/worker/tasks/main.yaml
```bash
- name: Copy custom script to local bin
   copy:
    src: files/my_custom_script.sh
    dest: /usr/local/bin/my_custom_script.sh
    owner: root
    group: root
    mode: '0744'
   notify: run_fuction_handler                   <== You can use notify similar to function calls
```

### roles/worker/handlers/main.yaml
```bash
- name: run_fuction_handler                      <== Make sure name matches the notify module caller
  command: echo 'This handler was runnn from notify module'
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
changed: [192.168.2.240]                                                                             <== This has change. So, notify module will trigger

RUNNING HANDLER [worker : run_fuction_handler] **********************************                    <== See handlers being called if there are changes
changed: [192.168.2.240]

PLAY RECAP **********************************************************************
192.168.2.240              : ok=5    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.2.243              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>
