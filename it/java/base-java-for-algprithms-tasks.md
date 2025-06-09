
## String/char
длина строка 
```java
int len = s.length();
```
получить символ по индексу
```java
char ch = s.charAt(0);
```

число или буква
```java
boolean b = Character.isLetterOrDigit(s.charAt(l))
```

к нижнему регистру
```java
char ch = Character.toLowerCase(s.charAt(l))
```
## Collections
размер списка
```java
List<Integer> list = new ArrayList<>();
list.size();
```

получить элемент списка по индексу
```java
list.get(7);
```

развернуть список
```java
Collections.reverse(list);
```

Конвертация array[] , List<>
#array #list #convert
```java
List<String> wordsList = Arrays.asList("I", "love", "learning");
String[] wordsArray = wordsList.toArray();
```