
---

## Системные колонки

`ctid`
Физическое расположение данной версии строки в таблице. Заметьте, что хотя по `ctid` можно очень быстро найти версию строки, значение `ctid` изменится при выполнении `VACUUM FULL`. Таким образом, `ctid` нельзя применять в качестве долгосрочного идентификатора строки. Для идентификации логических строк следует использовать первичный ключ

```sql
select ctid from operation
```

результат:
```
| ctid |  
| :--- |  
| \(0,1\) |  
| \(0,2\) |  
...
| \(0,32\) |  
| \(0,33\) |  
| \(1,1\) |  
| \(1,2\) |  
...
```

---

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
```#