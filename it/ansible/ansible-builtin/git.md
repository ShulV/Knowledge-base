>Этот модуль является частью `ansible-core` и включен во все установки Ansible. В большинстве случаев вы можете использовать краткое название модуля git даже без указания ключевого слова `collections`. Однако мы рекомендуем вам использовать полное имя коллекции (FQCN) `ansible.builtin.git` для удобства ссылки на документацию по модулю и во избежание конфликтов с другими коллекциями, которые могут иметь такое же имя модуля.

task exmaple:
```yml
- name: Git checkout
  ansible.builtin.git:
    repo: 'https://github.com/ansible/ansible.git'
    dest: /tmp/checkout
    version: release-0.22

- name: Read-write git checkout from github
  ansible.builtin.git:
    repo: git@github.com:ansible/ansible.git
    dest: /tmp/checkout
```