#index 

## Список возможных индексов (методов доступа)
#list #index #btree #gist #brin #gin #hash #heap #access
получить список индексов, которые есть у вашего постгреса:
```sql
select amname from pg_am;
```
вывод:
```bash
+------+  
|amname|  
+------+  
|heap  |  
|btree |  
|hash  |  
|gist  |  
|gin   |  
|spgist|  
|brin  |  
+------+
```

>P.S. heap - не индекс, а обычное сканирование последовательности
>AM - access methods

**Индексов в postgres17 - 6 штук., методов доступа - 7**
## Свойства методов доступа
#index #prop #properties #property #order #unique #multi_col #exclude

- **can_order**  Метод доступа позволяет указать порядок сортировки значений при создании индекса (в настоящее время применимо только для btree);
- **can_unique**  Поддержка ограничения уникальности и первичного ключа (применимо только для btree);
- **can_multi_col**  Индекс может быть построен по нескольким столбцам;
- **can_exclude**  Поддержка ограничения исключения EXCLUDE.

| тип    | can_order | can_unique | can_multi_col | can_exclude |
| ------ | --------- | ---------- | ------------- | ----------- |
| btree  | +         | +          | +             | +           |
| hash   | -         | -          | -             | +           |
| gin    | -         | -          | +             | -           |
| gist   | -         | -          | +             | +           |
| spgist | -         | -          | -             | +           |
| brin   | -         | -          | +             | -           |

> Получить эту информацию  можно таким запросом:
```sql
select a.amname, p.name, pg_indexam_has_property(a.oid,p.name)  
from pg_am a,  
     unnest(array['can_order','can_unique','can_multi_col','can_exclude']) p(name)  
where a.amname = 'btree' order by a.amname;
```

## Свойства индексов
#prop #index #property 
- **clusterable**  Возможность переупорядочивания строк таблицы в соответствии с данным индексом (кластеризация одноименной командой CLUSTER);
- **index_scan**  Поддержка индексного сканирования. Это свойство может показаться странным, однако не все индексы могут выдавать TID по одному — некоторые выдают все результаты сразу и поддерживают только сканирование битовой карты;
- **bitmap_scan**  Поддержка сканирования битовой карты;
- **backward_scan**  Выдача результата в порядке, обратном указанному при создании индекса.

---
## Функциональные индексы
#expression #index #function #functional #func #bitmap #seq #scan

```bash
postgres=# explain (costs off) select * from t where lower(b) = 'a';  
                QUERY PLAN                  
------------------------------------------  
 Seq Scan on t  
   Filter: (lower((b)::text) = 'a'::text)  
(2 rows)
```

> тут индекс не используется, чтобы использовался, нужно добавить ФУНКЦИОНАЛЬНЫЙ ИНДЕКС
условие поиска должно иметь вид **«_индексированное-поле оператор выражение_**»

```bash
postgres=# create index on t(lower(b));  
CREATE INDEX  
postgres=# analyze t;  
ANALYZE  
postgres=# explain (costs off) select * from t where lower(b) = 'a';  
                     QUERY PLAN                      
----------------------------------------------------  
 Bitmap Heap Scan on t  
   Recheck Cond: (lower((b)::text) = 'a'::text)  
   ->  Bitmap Index Scan on t_lower_idx  
         Index Cond: (lower((b)::text) = 'a'::text)  
(4 rows)
```

> Функциональный индекс создается не по полю таблицы, а по произвольному выражению; оптимизатор будет принимать во внимание такой индекс для условий вида **«_индексированное-выражение оператор выражение_»**

---
## Индексы по нескольким полям (многоколоночные индексы)
#multi #index #multicolumn #fields
```bash
postgres=# create index on t(a,b);
```

---
## Частичные индексы
#part #partition #index
```bash
postgres=# create index on t(c) where c;
```