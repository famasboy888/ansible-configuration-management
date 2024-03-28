# Ansible Day-1

```bash
ansible all --key-file ~/key_pair.pem --user debian -i inventory -m ping
```

```bash
Output:
+ 192.168.2.243 | $${\color{lightgreen}SUCCESS}$$ => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

