## Монтирование директорий
#mount #volume #bind #tmpfs
Вы можете подключить (смонтировать, mount) к контейнеру разные типы хранилищ:

- **bind**
    - менее строгий вариант
    - данные может изменять как контейнер докер, так и любые другие _non-docker_ процессы (вы сможете через “проводник” создавать или удалять файлы)
    - папку _создаете вы сами_ вручную (а не docker)
    - можно “шарить” данные между контейнерами
    - удобно использовать при локальной разработке и тестировании приложений
- **volume**
    - более строгий вариант
    - данные может изменять **только** докер контейнер
    - вы **не** сможете через “проводник” создавать или удалять файлы
    - папку создает сам _docker_ в своей “песочнице”
    - можно “шарить” данные между контейнерами
    - удобно использовать в боевом режиме приложения (чтобы никто случайно не смог испортить данные в папке)
    - часто вместо _volume_ используют слово **“том”** (перевод с англ.)
- **tmpfs**
    - временное хранение данных в памяти
    - намного быстрее доступ, чем к обычным файлам
    - нельзя “зашарить” данные между контейнерами

---
## Cети в докер
#docker #network 

1) bridge (по умолчанию)
2) host
3) none
4) ...

---

