#selinux

**SELinux (SELinux)** — это система принудительного контроля доступа, реализованная на уровне ядра.

P.S. обычно просто переводим в permissive и не настраиваем
```bash
$ sestatus
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   permissive
Mode from config file:          permissive
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Memory protection checking:     actual (secure)
Max kernel policy version:      33
```
## Режимы
#selinux #mode #premissive #enforcing #warning #strict #linux
1. **Enforcing** — запрет доступа на основании правил политики.
2. **Permissive** — ведение лога действий, нарушающих политику, которые в режиме enforcing были бы запрещены.
3. **Disabled** — полное отключение SELinux.

временно переключить режим
```bash
sudo setenforce Permissive
```
включить режим `permissive` на постоянной основе
```bash
sudo sed -i 's/SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config
```
##### Чем отличается каждый режим?
- **Strict mode (Enforcing)**:
    - Политики безопасности применяются жёстко, и любые попытки нарушения установленных ограничений приводят к отказу операции.
    - Нарушения протоколируются в журнале (`audit.log`).
- **Warning mode (Permissive)**:
    - Все ограничения продолжают проверяться, но нарушители пропускаются и разрешают выполнение операций.
    - Любые предупреждения записываются в журнал, но никаких реальных действий не предпринимается против попыток нарушений.
- Disabled только через конфиг  `/etc/selinux/config` 

## Лог ошибок
`/var/log/audit/audit.log`
команда для  поиска ошибок
```
audit2why < /var/log/audit/audit.log
```
## Переключатели политик
```
semanage boolean -l
```

## Посмотреть метки
```
ls -Z /etc/httpd
```

## Проверка контекста
```
sudo semanage fcontext -l | grep '/var/www'
```

пример изменения контекста
```
$ semanage fcontext -a -t httpd_sys_content_t ‘/home/victor/html(/.*)?’
$ semanage fcontext -l | grep ‘/home/victor/html’
/home/victor/html(/.*)? all files system_u:object_r:httpd_sys_content_t:s0
$ restorecon -Rv /home/victor/html
```