

## Встраивание
#inline #inlining


```html
<p>Hello, [[${session.user.name}]]!</p>
```

```html
<p>Hello, <span th:text="${session.user.name}">Sebastian</span>!</p>
```


Выражения между [[...]] или [(...)] считаются встроенными выражениями, и внутри них мы можем использовать любое выражение, которое также было бы действительным в атрибуте **th:text** или **th:utext**.