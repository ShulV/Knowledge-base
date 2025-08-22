#playbook #ansible

---
#file #create
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

#execute #playbook
Запуск плейбука:
```bash
shulpov.v@fedora:~/IdeaProjects/ansible-probe/ansible_quickstart$ ansible-playbook -i inventory.yaml playbook.yaml
```

P.S. OK=3 указывает на то, что каждая задача выполнена успешно.

---

## Запуск с выбором инвентарей
```bash
ansible-playbook get_logs.yml -i staging -i production
```
`-i` - используется для задания инвентарного файла (или нескольких файлов). Если этот параметр не указан, Ansible будет искать стандартный инвентарь в `/etc/ansible/hosts` или в папке проекта.