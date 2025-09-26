>Этот модуль является частью `ansible-core` и включен во все установки Ansible. В большинстве случаев вы можете использовать краткое название модуля `shell` даже без указания ключевого слова `collections`. Однако мы рекомендуем вам использовать полное имя коллекции (FQCN) `ansible.builtin.shell` для удобства ссылки на документацию по модулю и во избежание конфликтов с другими коллекциями, которые могут иметь такое же имя модуля.


task example:
```yml
- name: Make "chmod u+x" for activemq subfolders  
  shell: 'find {{ root_install_folder }}/{{ username }} -type d -exec chmod u+x {} \;'
```