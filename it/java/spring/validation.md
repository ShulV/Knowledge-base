## Влидация с помощью аннотаций
#bindingresult #binding #validate #validation #argument

`MethodArgumentNotValidException`
не кидается, когда после валидируемого параметра стоит BindingResult. Вместо исключение ошибки сетятся в данный объект. Данный объект является сигналом спрингу, что разработчик сам проведет обработку ошибку без исключения.
BindingResult должен быть после валидируемого объекта, иначе не будет работать.