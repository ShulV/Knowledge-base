## механизмы динамического проксирования
(**байт-код инструментами для AOP**)
#proxy #dynamic #cglib #aspectj #byte #buddy #byte_buddy #aop #byte_code

|Библиотека|Подход|Преимущества|Ограничения|
|---|---|---|---|
|CGLIB|Подклассы-прокси (динамически после компиляции)|Простота в Spring AOP|Устарел, final-классы, только публичные методы [javarush](https://javarush.com/quests/lectures/questspring.level01.lecture61)​|
|AspectJ|Weaving байт-кода (compile-time, post-compile или динамически на загрузке)|Полный AOP, любые join points|Требует компилятора/JVM-аргументов [panlw.github+1](https://panlw.github.io/15277821532847.html)​|
|Byte Buddy|Динамическая генерация классов (после компиляции на runtime)|Быстрый, гибкий, современный API|Меньше фокуса на AOP, больше на инструментах [credera](https://www.credera.com/en-us/insights/aspect-oriented-programming-in-spring-boot-part-2-spring-jdk-proxies-vs-cglib-vs-aspectj)​|