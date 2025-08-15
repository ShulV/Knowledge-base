- **ansible-core**: базовая функциональность и модули Ansible,
- **ansible-collections**: коллекция дополнительных модулей и подключаемых компонентов.

## Версии
https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#ansible-core-support-matrix

|Ansible Community Package Release|Status|Core version dependency|
|---|---|---|
|12.0.0|In development (unreleased)|2.19|
|[11.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/11/CHANGELOG-v11.md)|Current|2.18|
|[10.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/10/CHANGELOG-v10.md)|EOL after 10.7|2.17|
|[9.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/9/CHANGELOG-v9.rst)|EOL after 9.13|2.16|
|[8.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/8/CHANGELOG-v8.rst)|Unmaintained (end of life)|2.15|
|[7.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/7/CHANGELOG-v7.rst)|Unmaintained (end of life)|2.14|
|[6.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/6/CHANGELOG-v6.rst)|Unmaintained (end of life)|2.13|
|[5.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/5/CHANGELOG-v5.rst)|Unmaintained (end of life)|2.12|
|[4.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/4/CHANGELOG-v4.rst)|Unmaintained (end of life)|2.11|
|[3.x Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/3/CHANGELOG-v3.rst)|Unmaintained (end of life)|2.10|
|[2.10 Changelogs](https://github.com/ansible-community/ansible-build-data/blob/main/2.10/CHANGELOG-v2.10.rst)|Unmaintained (end of life)|2.10|

| Ansible core version                                                                       | Support                                                                   | End Of Life                | Control Node Python                | Target Python / PowerShell                                          |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- | -------------------------- | ---------------------------------- | ------------------------------------------------------------------- |
| [2.18](https://github.com/ansible/ansible/blob/stable-2.18/changelogs/CHANGELOG-v2.18.rst) | GA: 04 Nov 2024<br><br>Critical: 19 May 2025<br><br>Security: 03 Nov 2025 | May 2026                   | Python 3.11 - 3.13                 | Python 3.8 - 3.13<br><br>PowerShell 5.1                             |
| [2.17](https://github.com/ansible/ansible/blob/stable-2.17/changelogs/CHANGELOG-v2.17.rst) | GA: 20 May 2024<br><br>Critical: 04 Nov 2024<br><br>Security: 19 May 2025 | Nov 2025                   | Python 3.10 - 3.12                 | Python 3.7 - 3.12<br><br>PowerShell 5.1                             |
| [2.16](https://github.com/ansible/ansible/blob/stable-2.16/changelogs/CHANGELOG-v2.16.rst) | GA: 06 Nov 2023<br><br>Critical: 20 May 2024<br><br>Security: Nov 2024    | **EOL**<br><br>July 2025   | Python 3.10 - 3.12                 | Python 2.7<br><br>Python 3.6 - 3.12<br><br>Powershell 5.1           |
| [2.15](https://github.com/ansible/ansible/blob/stable-2.15/changelogs/CHANGELOG-v2.15.rst) | GA: 22 May 2023<br><br>Critical: 06 Nov 2023<br><br>Security: 20 May 2024 | **EOL**<br><br>Nov 2024    | Python 3.9 - 3.11                  | Python 2.7<br><br>Python 3.5 - 3.11<br><br>PowerShell 3 - 5.1       |
| [2.14](https://github.com/ansible/ansible/blob/stable-2.14/changelogs/CHANGELOG-v2.14.rst) | GA: 07 Nov 2022<br><br>Critical: 22 May 2023<br><br>Security: 06 Nov 2023 | **EOL**<br><br>20 May 2024 | Python 3.9 - 3.11                  | Python 2.7<br><br>Python 3.5 - 3.11<br><br>PowerShell 3 - 5.1       |
| [2.13](https://github.com/ansible/ansible/blob/stable-2.13/changelogs/CHANGELOG-v2.13.rst) | GA: 23 May 2022<br><br>Critical: 07 Nov 2022<br><br>Security: 22 May 2023 | **EOL**<br><br>06 Nov 2023 | Python 3.8 - 3.10                  | Python 2.7<br><br>Python 3.5 - 3.10<br><br>PowerShell 3 - 5.1       |
| [2.12](https://github.com/ansible/ansible/blob/stable-2.12/changelogs/CHANGELOG-v2.12.rst) | GA: 08 Nov 2021<br><br>Critical: 23 May 2022<br><br>Security: 07 Nov 2022 | **EOL**<br><br>22 May 2023 | Python 3.8 - 3.10                  | Python 2.6 - 2.7<br><br>Python 3.5 - 3.10<br><br>PowerShell 3 - 5.1 |
| [2.11](https://github.com/ansible/ansible/blob/stable-2.11/changelogs/CHANGELOG-v2.11.rst) | GA: 26 Apr 2021<br><br>Critical: 08 Nov 2021<br><br>Security: 23 May 2022 | **EOL**<br><br>07 Nov 2022 | Python 2.7<br><br>Python 3.5 - 3.9 | Python 2.6 - 2.7<br><br>Python 3.5 - 3.9<br><br>PowerShell 3 - 5.1  |
| [2.10](https://github.com/ansible/ansible/blob/stable-2.10/changelogs/CHANGELOG-v2.10.rst) | GA: 13 Aug 2020<br><br>Critical: 26 Apr 2021<br><br>Security: 08 Nov 2021 | **EOL**<br><br>23 May 2022 | Python 2.7<br><br>Python 3.5 - 3.9 | Python 2.6 - 2.7<br><br>Python 3.5 - 3.9<br><br>PowerShell 3 - 5.1  |
| [2.9](https://github.com/ansible/ansible/blob/stable-2.9/changelogs/CHANGELOG-v2.9.rst)    | GA: 31 Oct 2019<br><br>Critical: 13 Aug 2020<br><br>Security: 26 Apr 2021 | **EOL**<br><br>23 May 2022 | Python 2.7<br><br>Python 3.5 - 3.8 | Python 2.6 - 2.7<br><br>Python 3.5 - 3.8<br><br>PowerShell 3 - 5.1  |

- [ ] ansible должен быть установлен на управляемой машине, т.е. у меня, если я обновляю клиентов?
- [x] версия python на моей машине и на удаленной машине (куда деплоим) должна соответствовать таблице выше

#### деинсталляция
```bash
pipx uninstall ansible
pipx uninstall ansible-core
```
#### виртуальное окружение для старого ansible
#virtual #env #virtualenv
создать
```bash
shulpov.v@fedora:~$ virtualenv -p python env_ansible
created virtual environment CPython3.13.3.final.0-64 in 94ms
  creator CPython3Posix(dest=/home/shulpov.v/env_ansible, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, via=copy, app_data_dir=/home/shulpov.v/.local/share/virtualenv)
    added seed packages: pip==25.1.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator
```
перейти
```bash
shulpov.v@fedora:~$ source env_ansible/bin/activate
(env_ansible) shulpov.v@fedora:~$ 
```
(нашел ansible с нужным ansbile-core 9.* -> 2.16)
```bash
(env_ansible) shulpov.v@fedora:~$ pip install 'ansible==9.13.0'
Collecting ansible==9.13.0
....

(env_ansible) shulpov.v@fedora:~$ ansible --version
ansible [core 2.16.14]
```
