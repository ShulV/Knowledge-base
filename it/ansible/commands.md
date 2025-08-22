## check mode

В этом режиме ансибл не изменяет удаленные ноды, только выводит команды

```bash
ansible all -m copy -a "content=foo dest=/root/bar.txt" -C
```
(`-C` or `--check`)  - ансибл не создает и не обновляет `/root/bar.txt` 