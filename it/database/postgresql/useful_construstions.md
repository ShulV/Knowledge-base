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

## Посмотреть количество коннектов на сервере
#connect #sql #stat #activity #datname #application #pool #connection

по коннектам к базам данных на сервере
```sql
SELECT count(*), datname FROM pg_stat_activity group by datname;
```

по коннектам приложений к базам
```sql
select application_name, COUNT(*) as count from pg_stat_activity group by application_name
```


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

