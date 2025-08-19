Создали инвентарь в корне (файл inventory.yaml):
```yml
myhosts:  
  hosts:  
    45.130.146.99:  
      ansible_user: victor  
    192.0.2.50:  
      ansible_user: shulpov.v
```

---

Верифицируем файл:
```bash
shulpov.v@fedora:~/IdeaProjects/ansible-probe/ansible_quickstart$ ansible-inventory -i inventory.yaml --list
{
    "_meta": {
        "hostvars": {
            "192.0.2.50": {
                "ansible_user": "shulpov.v"
            },
            "45.130.146.99": {
                "ansible_user": "victor"
            }
        }
    },
    "all": {
        "children": [
            "ungrouped",
            "myhosts"
        ]
    },
    "myhosts": {
        "hosts": [
            "45.130.146.99",
            "192.0.2.50"
        ]
    }
}

```
P.S. если бы не прошли проверки получили бы, например предупреждение:
```bash
[WARNING]: Skipping unexpected key (hosts3) in group (myhosts), only "vars", "children" and "hosts"
are valid
```

---

Пингуем группу хостов инвентаря:
```bash
shulpov.v@fedora:~/IdeaProjects/ansible-probe/ansible_quickstart$ ansible myhosts -m ping -i ./inventory.yaml
45.130.146.99 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.0.2.50 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.0.2.50 port 22: Connection timed out",
    "unreachable": true
}

```

---
Создали плейбук в корне (playbook.yaml):
```yaml
- name: My first play  
  hosts: myhosts  
  tasks:  
    - name: Ping my hosts  
      ansible.builtin.ping:  
  
    - name: Print message  
      ansible.builtin.debug:  
        msg: Hello world
```

Запуск плейбука:
```bash
shulpov.v@fedora:~/IdeaProjects/ansible-probe/ansible_quickstart$ ansible-playbook -i inventory.yaml playbook.yaml
```

P.S. OK=3 указывает на то, что каждая задача выполнена успешно.

