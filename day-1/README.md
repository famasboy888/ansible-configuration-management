# Ansible Day-1

```bash
ansible all --key-file ~/key_pair.pem --user debian -i inventory -m ping
```
<h1 style="color: red">Output:</h1>

```bash
 192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

