# Ansible Day-4

## Run Service in instance

Reference for **[Service Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)**.

Created custom service **my_custom_service.service** that will run **my_custom_script.sh**.

All this files will be copied to instance in specific directories

```bash
---

- hosts: master
  become: true
  tasks:

  - name: Copy custom script to local bin
    tags: debian
    copy:
      src: files/my_custom_script.sh
      dest: /usr/local/bin/my_custom_script.sh
      owner: root
      group: root
      mode: '0744'

  - name: Copy custom service to systemd
    tags: debian
    copy:
      src: files/my_custom_service.service
      dest: /etc/systemd/system/my_custom_service.service
      owner: root
      group: root
      mode: '0644'

  - name: Start custom service
    tags: debian
    service:                                <== This will run a service in the instance
        name: my_custom_service             <== This refers to my_custom_service.service
        state: started
        enabled: true                       <== Make this persistent to restarts
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
ansible-playbook --tags debian add_custom_service.yaml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
PLAY [master] *******************************************************************

TASK [Gathering Facts] **********************************************************
ok: [192.168.2.243]

TASK [Copy custom script to local bin] ******************************************
ok: [192.168.2.243]

TASK [Copy custom service to systemd] *******************************************
changed: [192.168.2.243]

TASK [Start custom service] *****************************************************
changed: [192.168.2.243]

PLAY RECAP **********************************************************************
192.168.2.243              : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>

<img width="1280" alt="OpenStack" src="https://github.com/famasboy888/ansible-configuration-management/assets/23441168/7d79f9ad-d4af-43a6-a9f9-775988729a9c">






