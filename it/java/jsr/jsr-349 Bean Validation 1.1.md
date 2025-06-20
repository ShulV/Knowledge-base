- **Год выпуска**: 2013 г.
- **Цель**: Создание единого универсального API для валидации Java-объектов независимо от среды выполнения (web, EE, SE).

  
При переходе с JSR-303 на JSR-349, вероятно, потребуется внести минимальные изменения в код. Наиболее значительные отличия включают:

- **Метод-уровневая валидация**: Появилась возможность аннотировать параметры и возвращаемые значения методов для проверки их правильности. Например, аннотация `@Valid` стала доступной для параметров и возвращаемого значения метода.
- **Группа преобразования**: Введено преобразование между группами валидации, что позволяет изменять группу валидации на ходу.
- **EL-выражения**: Возможна интерполяция сообщений об ошибках с использованием Expression Language (EL), что улучшает гибкость формулировки сообщений.
- **Интеграция с CDI**: Если ваше приложение использует CDI, JSR-349 предоставляет новую интеграционную точку для внедрение компонентов Bean Validation.

В основном, основное влияние коснется использования новой функциональности, но существующий код с аннотациями вроде `@NotNull`, `@Size`, и т.п., останется рабочим.

> P.S. ОСНОВНОЕ ТУТ @Valid на параметрах

---
