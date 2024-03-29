# Ansible Day-8

## Run Service in instance

Reference for **[User Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/user_module.html)**.

Reference for **[Authorize Key Module](https://docs.ansible.com/ansible/latest/collections/ansible/posix/authorized_key_module.html)**.

Reference for **[Copy Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)**.

```bash
- hosts: master
  become: true
  tasks:

  - name: Create user called ops
    tags: debian
    user:                                                                                  <== creates a user "ops"
      name: ops
      groups: root

  - name: add SSH keys for ops
    tags: debian
    authorized_key:                                                                        <== creates/sends authorzied ssh key for instance  
      user: ops
      key: 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDR0ceaIXMZSQPx/J5p6zaDCTpZmQEB>

  - name: add sudoer file
    tags: debian
    copy:                                                                                 <== Create sudoers file to have no password
      src: files/sudoer_ops
      dest: /etc/sudoers.d/ops
      owner: root
      group: root
      mode: '0440'
```

**Run command: And target debian tag**
```bash
ansible-playbook --tags debian make_user.yaml
```

<details>
  <summary><i>Output</i></summary>
$${\color{green}Output:}$$

```bash
PLAY [master] *******************************************************************

TASK [Gathering Facts] **********************************************************
ok: [192.168.2.243]

TASK [Create user called ops] ***************************************************
changed: [192.168.2.243]

TASK [add SSH keys for ops] *****************************************************
changed: [192.168.2.243]

TASK [add sudoer file] **********************************************************
changed: [192.168.2.243]

PLAY RECAP **********************************************************************
192.168.2.243              : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
</details>
