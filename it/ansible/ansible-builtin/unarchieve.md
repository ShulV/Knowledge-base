>Этот модуль является частью `ansible-core` и включен во все установки Ansible. В большинстве случаев вы можете использовать краткое название модуля unarchive даже без указания ключевого слова `collections`. Однако мы рекомендуем вам использовать полное имя коллекции (FQCN) `ansible.builtin.unarchive` для удобства привязки к документации по модулю и во избежание конфликтов с другими коллекциями, которые могут иметь такое же имя модуля.

task example:
```yml
- name: Unpack "activemq.zip"  
  unarchive:  
    src: "{{ root_install_folder }}/{{ username }}/activemq.zip"  
    dest: "{{ root_install_folder }}/{{ username }}"  
    remote_src: yes  
    owner: "{{ username }}"  
    group: "{{ username }}"  
  no_log: True
```