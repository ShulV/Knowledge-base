## Пример удаления дубликатов
#duplicate #delete #ctid 
```sql
-- удаление всех товаров-дубликатов (1-ый остается)
DELETE FROM merchant_request_info mri USING (
SELECT MIN(ctid) as ctid, merchant_request, name, quantity, "sum"
FROM merchant_request_info
GROUP BY (merchant_request, name, quantity, "sum") HAVING COUNT(*) > 1
) first_from_duplicates
WHERE mri.merchant_request = first_from_duplicates.merchant_request
AND mri.name = first_from_duplicates.name
AND mri.quantity = first_from_duplicates.quantity
AND mri.sum = first_from_duplicates.sum
AND mri.ctid <> first_from_duplicates.ctid;
```
> **ctid** - это ==скрытое системное поле, которое представляет собой уникальный идентификатор физического расположения строки в таблице==. Он состоит из двух чисел: номера блока (страницы) и смещения внутри этого блока, где хранится строка.

---
## Условные UNIQUE
#conditional #partitial #index #unique

Создание частичного уникального индекса осуществляется следующим образом:

```sql
CREATE UNIQUE INDEX stop_myc ON stop (col_a) WHERE (col_b = 1);
```

```sql
CREATE UNIQUE INDEX client_login_case_deleted_idx ON client USING btree (login, (  
CASE deleted  
    WHEN 1 THEN NULL::integer  
    ELSE 1  
END));
```
для каждого активного клиента уникальный логин. Для удалённых клиентов этот индекс не применяется, и они могут иметь повторяющиеся логины.

---

## Ограничение для запрета строк с пробелами
#space #regexp #check #constraint

```sql
ALTER TABLE baas.client_account ADD CONSTRAINT no_spaces_in_iban_check CHECK (iban ~* '^[^ ]+$');
```
`^` - начало строки
`+` - пробельный символ должен встретиться 1 или более раз (`*` - 0 и более раз)
P.S. можно использовать `*` - пробельный символ должен встретиться 0 или более раз
`[^ ]` — отрицательная группа символов, которая значит "любые символы, кроме пробела"
`$` - конец строки

---

## Равенство любому из элементов списка с возможностью передачи пустого списка
#empty #null #any #array
```sql
--...
WHERE 
(:labelIdsAreEmpty OR owl.workspace_label = ANY(ARRAY[:labelIdArray]))  
AND (:statusesAreEmpty OR o.state         = ANY(ARRAY[:statusArray]))  
AND (:providerTypesAreEmpty OR pt.code     = ANY(ARRAY[:providerTypeArray]) )
```

P.S. через `WHERE IN (...)` получается не очень, т.к. туда что-то нужно передавать
через ANY(ARRAY[]) можно передавать пустой массив
> Удобно использовать для фильтров.

---
## serial значения отстали
#setval #nextval #currval #sequence #max
```sql
select nextval('permission_section_id_seq');-- для инициализации перед вызовом setval. Значение все равно затрет setval, так что эта команда не влияет на значение
select setval('permission_section_id_seq', (select max(id) from permission_section));
```

P.S. был случай, когда вставляли значения в таблицу, используя в качестве значения id `max(id)`, таким образом sequence не поднимался, а потом падал, когда делали вставку с использованием встроенного `nextval

```sql
select currval('permission_section_id_seq');--тоже падал без инициализации
```

---
## Порядковые номера
#row_number 
```sql
SELECT ca.id AS account_id,  
       ca.account_number AS old_account_number,  
       cl.id AS client_id,  
       cl.login,  
       ROW_NUMBER() OVER(PARTITION BY cl.id ORDER BY ca.id) AS account_sequence_number  
  FROM client_account ca  
  JOIN client cl ON ca.client = cl.id
```

`PARTITION BY` - чтобы для каждой партиции (секции) отчёт начинался с единицы
`ORDER BY ca.id` - принцип установки порядкового номера

P.S. тут получаем порядковые номера аккаунтов для конкретных клиентов. Т.е. если у клиента 3 аккаунта, будут порядковые номера 1, 2 и 3.

---
## автоинкремент
#serial #generated #identity #always
**1) GENERATED ALWAYS AS IDENTITY**
> гибкий вариант автоинкремента
```sql
id integer generated always as identity (minvalue 5 increment by 2 maxvalue 1000 cache 10000000 cycle)
```

**2) SERIAL**
> простой и удобный для большинства случаев, создает скрытую последовательность 
```sql
id BIGSERIAL
-- скрытая последовательность BIGINT NOT NULL DEFAULT nextval('sequence_name')
```

---

## Разные способы получить временную метку
#time #date #now #timestamp #clock #current_timestamp #clock_timestamp
- **CURRENT_TIMESTAMP / NOW():**
    - Возвращают фиксированное значение начала транзакции.
    - Удобны для операций, зависящих от единого значения времени на весь период транзакции.
- **CLOCK_TIMESTAMP():**
    - Всегда возвращает точное текущее время.
    - Обновляет значение каждый раз при каждом новом вызове.

---

## Вставка N строк
#loop #for #insert #random #postgres
```sql
insert into probe.test(id, "name")  
select s.id, (s.id::varchar)  
from generate_series(1,1000000) as s(id)  
order by random();
```

---
## Индекс на колонку на уникальность
#unique #constraint #index #idx
```sql
create unique index if not exists  
    client_workspace_role_code_idx on client_workspace_role (code);
```

---
