
---
## Инициализация нового репозитория
#git #init #initialization #инициализация
```bash
git init
```
P.S. можно начать делать всё локально, а привязать репозиторий уже позже

---
## Связка локального и удалённого репозитория
#git #remote #origin #связь #связка
```bash
# привязка
git remote add origin https://github.com/username/repository.git
# проверка, какие удаленные репо связаны с вашим локальным репо
git remote -v
# отправка коммитов в удаленный репо
git push -u origin main
```

---
## Создание пустого коммита
#commit #empty #пустой 
```bash
git --allow-empty -m "empty commit"
```
P.S. так можно запустить CI, если он настроен на push в определенную ветку

---

##
