- explain
- explain (costs off)
- explain analyze


## Виды сканирования
- Индексное сканирование
```sql
explain (costs off) select * from t where a = 1;

Index Scan using t_a_idx on t  
   Index Cond: (a = 1)  
(2 rows)
```
- Сканирование по битовой карте
```sql
explain (costs off) select * from t where a <= 100

Bitmap Heap Scan on t  
   Recheck Cond: (a <= 100)  
   ->  Bitmap Index Scan on t_a_idx  
         Index Cond: (a <= 100)  
(4 rows)
```
- Сканирование нескольких индексов сразу
```sql
 explain (costs off) select * from t where a <= 100 and b = 'a';
 
 Bitmap Heap Scan on t  
   Recheck Cond: ((a <= 100) AND (b = 'a'::text))  
   ->  BitmapAnd  
         ->  Bitmap Index Scan on t_a_idx  
               Index Cond: (a <= 100)  
         ->  Bitmap Index Scan on t_b_idx  
               Index Cond: (b = 'a'::text)  
(7 rows)
```
> P.S. объединяются 2 битмапы

- Последовательное сканирование
```sql
 explain (costs off) select * from t where a <= 40000;
 
 Seq Scan on t  
   Filter: (a <= 40000)  
(2 rows)
```

- Покрывающие индексы
```sql
explain (costs off) select a from t where a < 100;

 Index Only Scan using t_a_idx on t  
   Index Cond: (a < 100)  
(2 rows)
```
---
## Проверить упорядоченность
#stats #correlation #postgres
```sql
select attname, correlation from pg_stats where tablename = 't';
```

 attname | correlation
 -------------+-----------------
 b              |    0.533512    
 c              |    0.942365    
 a              | -0.00768816
 (3 rows)
 
Значения, близкие по модулю к единице, говорят о высокой упорядоченности (как для столбца c), а близкие к нулю — наоборот, о хаотичном распределении (столбец a).

> индексы используют запрос такого вида для определения лучшего вида сканирования

---
