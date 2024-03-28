# Ansible Day-1

## Initial run
```bash
ansible all --key-file ~/key_pair.pem --user debian -i inventory -m ping
```
<hr>

$${\color{green}Output:}$$

```bash
192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## Running with local ansible.cfg
```bash
ansible all -m ping
```
<hr>

$${\color{green}Output:}$$

```bash
192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
