
---

## Денормализация

- вынесение расчетных данных в колонки (чтобы не тратить время на расчет)
- вынесение расчетных данных в отдельные таблицы
- создание отдельной БД для статистики

---
## Индексы
...

---
## Партиционирование таблиц
#partition 
...

---

## Динамическая денормализация
```sql
CREATE TABLE IF NOT EXISTS external_ident_sys_response (
	id BIGSERIAL PRIMARY KEY,
	req_priv_change BIGINT NOT NULL,
	content JSONB NOT NULL,
	attempt_id VARCHAR(64) GENERATED ALWAYS AS ((content->>'attemptId')) STORED,
	review_status VARCHAR(64) GENERATED ALWAYS AS ((content->>'reviewStatus')) STORED,
	date_add TIMESTAMPTZ NOT NULL DEFAULT now(),
	
	CONSTRAINT ext_ident_resp_keys_chk
	CHECK (attempt_id IS NOT NULL AND review_status IS NOT NULL),
	CONSTRAINT ext_ident_resp_attempt_status_uk
	UNIQUE (attempt_id, review_status)
);
```

`GENERATED ALWAYS AS` дублирование расчетных данных в доп. колонку\

---
## Резкое ухудшение производительности
- планировщик пошёл по другому пути, потому что количество данных превысило некоторый лимит (для планировщик)
	в таком случае стоит сделать ANALYZE на текущей БД и на бэкапе, когда всё было хорошо

