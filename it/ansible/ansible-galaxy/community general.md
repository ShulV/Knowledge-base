## timezone
#timezone #ansible #galaxy #ansible-galaxy #time #clock
Таска на установку таймзону на управляемой ноде:
```yml
- name: Set timezone to Asia/Tokyo
  community.general.timezone:
    name: Asia/Tokyo
```

> Этот плагин является частью community.general collection (версия 1.3.6).
Для его установки использовать: `ansible-galaxy collection install community.general`.
Чтобы использовать его в плейбуке, указать: `community.general.timezone`.
