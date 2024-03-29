# Ansible Day-4

## Transfer files from Controller to Instance using Ansible using COPY module

Reference for **[Copy](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html#examples)**.

```bash
---

- hosts: master
  become: true
  tasks:

  - name: Installing on Debian master
    tags: debian
    package:
      name:
         - "{{ apache_package }}"
      state: latest
      update_cache: true

  - name: Copy and replace apache index.html
    tags: debian
    copy:                                            <== Copy module
      src: files/default_site.html                   <== source of file
      dest: /var/www/html/index.html                 <== destination insidde the instance. You can rename it by changing the final file name.
      owner: root                                    <== Name of the user that should own the filesystem object, as would be fed to chown.
      group: root                                    <== When left unspecified, it uses the current group of the current user unless you are root, in which case it can preserve the previous ownership.
      mode: '0644'                                   <== You must either add a leading zero so that Ansible’s YAML parser knows it is an octal number (like 0644 or 01777) or quote it (like '644' or '1777')    
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

TASK [Copy and replace apache index.html] ******************************************************************************
changed: [192.168.2.243]

PLAY [worker] **********************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [192.168.2.240]

PLAY RECAP *************************************************************************************************************
192.168.2.240              : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.2.243              : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>

<img width="685" alt="OpenStack" src="https://github.com/famasboy888/ansible-configuration-management/assets/23441168/25857b14-952b-4e73-b87f-9c54e51c07f9">






