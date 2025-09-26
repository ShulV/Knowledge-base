#j2 #jinja #template

> Этот модуль является частью `ansible-core` и включен во все установки Ansible. 
   В большинстве случаев вы можете использовать шаблон краткого названия модуля даже без указания ключевого слова `collections`.
   Однако мы рекомендуем вам использовать полное имя коллекции (FQCN) `ansible.builtin.template` для удобства ссылки на документацию по модулю 
   и во избежание конфликтов с другими коллекциями, которые могут иметь такое же имя модуля.

task exmaple:
```yml
- name: Templating "credentials.properties"  
  template:  
    src: roles/install-activemq/files/credentials.properties.j2  
    dest: "{{ root_install_folder }}/{{ username }}/conf/credentials.properties"  
    owner: "{{ username }}"  
    group: "{{ username }}"  
    mode: '640'
```