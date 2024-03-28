# Ansible Day-1

```bash
ansible all --key-file ~/key_pair.pem --user debian -i inventory -m ping
```
<span style="color:blue">some *blue* text</span>.

```bash
 192.168.2.243 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

