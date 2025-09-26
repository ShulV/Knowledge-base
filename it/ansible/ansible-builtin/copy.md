>Этот модуль является частью `ansible-core` и включен во все установки Ansible. В большинстве случаев вы можете использовать краткое название модуля copy даже без указания ключевого слова `collections`. Однако мы рекомендуем вам использовать полное имя коллекции (FQCN) `ansible.builtin.copy` для удобства ссылки на документацию по модулю и во избежание конфликтов с другими коллекциями, которые могут иметь такое же имя модуля.

task exmaple:
```yml
- name: Upload "activemq.zip" to server  
  copy:  
    src: "/tmp/activemq.zip"  
    dest: "{{ root_install_folder }}/{{ username }}/activemq.zip"  
    owner: '{{ username }}'  
    group: '{{ username }}'  
    mode: '400'
```