## Создание vault
```bash
EDITOR=nano ansible-vault create --vault-password-file password_probe inventories/probe/group_vars/all/vault.yml
```
## Редактирование vault
```bash
EDITOR=nano ansible-vault edit --vault-password-file password_probe inventories/probe/group_vars/all/vault.yml
```