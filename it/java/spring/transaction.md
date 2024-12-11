
----

## Checked и unchecked исключения в транзакциях
#rollback #rollbackFor #checked #unchecked #commit #transactional
По умолчанию Spring откатывает транзакции только в случае **непроверяемого** исключения. **Проверяемые** же считаются «восстанавливаемыми» из-за чего Spring вместо `rollback` делает `commit`.

Чтобы откатить транзакцию, нужно заменить проверяемое исключение (например, `Exception`) на непроверяемое исключение (например, `NullPointerException`). Либо можно переопределить атрибут `rollbackFor` у аннотации.



P.S. в Kotlin нет checked/unchecked, но транзакции работают аналогично JAVA!!!
