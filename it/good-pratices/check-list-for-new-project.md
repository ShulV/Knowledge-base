# Основные вещи, которые нужно настроить при создании нового проекта 
P.S. конечно, в реальных условиях нужно полагаться на то, сколько проект будет жить и не заниматься овер-инженерингом.

---
## Настройка непрерывной доставки (CD)
#cd #deploy #automatization #auto #start #начало #настройка #setting
например, чтобы при пуше в `main` приложение компилировалось и доставлялось на конечный сервер.
Лучше это делать на голом проекте.

#код_который_помещается_в_голове
>**"Ходячий скелет" (Walking skeleton)** - это реализация наименьшей возможной функциональности, которую можно автоматически создавать, развертывать и тестировать от начала до конца.

P.S. самый простой вариант и то, с чего можно начать - обычный скрипт, который запустит сборку проекта, а затем его запустит.

---

## Настройка логгирования
#log #logging #setting #настройка #start #начало
...

---

## Включить все сообщения об ошибках
#message #error #monitoring #ошибка #сообщение #код_который_помещается_в_голове
...


---

## Настроить Swagger
возможно определиться с разделами api, чтобы настроить конфигурацию

---

## Настроить миграции БД
#migration #db

P.S. liquibase или flyway

---

## Установка метрики "Цикломатическая сложность" для разработчиков
#metric #rule #код_который_помещается_в_голове 

P.S.
На практике для простоты можно оценить сложность следующим образом: за каждое логическое ветвление (`if`, `else`, `switch`, `case`, циклы) добавляется по единице к общей цикломатической сложности.

Число 7 - идеальный вариант, т.к. 7 - это порог объема рабочей памяти человеческого мозга.

Помогает прийти к "фрактальной" архитектуре, где на каждом уровне абстракции код помещается в голове.

- [ ] Найти анализатор

---

## Установить метрики размера методов для разработчиков
#metric #rule #код_который_помещается_в_голове 

P.S. 
на работе максимальной шириной кода считалось 130 символов.
про кол-во строк разговора не было, были пару методов на 800 строк. Это АД!

Нужно зафиксировать для разработчиков, чтобы размер метода не превышал какого-то значения.

В книге "Код, который помещается в голове" приводят пример с блоком 80x24.
Java, наверное, более многословный язык, думаю, нужно дать размер побольше.
Тем более практика показывает, что с кодом, где до 50-100 строк ещё нормально разбираться, тем более, если это какая-то валидация с бросанием исключений, где все довольно прозрачно.

ОГРАНИЧИТЬ ДЛЯ JAVA БЛОКОМ 130x50 (сам придумал)

- [ ] Найти анализатор

---

## Правило на запрета возврата null из метода
#rule #код_который_помещается_в_голове #марк_симан #сергей_немчинский
Лучше:
- оборачивать в Optional<> (элемент не найден, элемент пустой. Ситуация, где нормально, что нечего возвращать)
- кидать Exception (не нашли то, что должны были найти, что-либо неожиданное, неверные параметры)

Исключительные ситуации:
- что-то вроде метода поиска значения элемента в хэш-мапе. Там мы возвращаем значение ноды, которая вполне может иметь такое значение и это нормально.

---

## Определиться с основными кастомными исключениями проекта
#exception #custom

хорошие варианты, что встречал:
```java
//для того, чтобы кидать Listener'е очереди
public class RepeatMessageException extends RuntimeException

//главное исключение для апи, от него наследовать другие более конкретные...
public class XmapApiException extends RuntimeException

//для коммита транзакций
@Transactional(noRollbackFor = CommitServiceException.class)
public class CommitServiceException extends XmapApiException

//общее для ошибок текущего сервиса, додумать ещё...
public class ServiceException extends XmapApiException
```


