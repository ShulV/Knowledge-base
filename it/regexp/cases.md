## regexp для валидации JSON
#regexp #json #validate
```php
/
    (?(DEFINE)
        (?<ws>      [\t\n\r ]* )
        (?<number>  -? (?: 0|[1-9]\d*) (?: \.\d+)? (?: [Ee] [+-]? \d++)? )    
        (?<boolean> true | false | null )
        (?<string>  " (?: [^\\\\"\x00-\x1f] | \\\\ ["\\\\bfnrt\/] | \\\\ u [0-9A-Fa-f]{4} )* " )
        (?<pair>    (?&ws) (?&string) (?&ws) : (?&value) )
        (?<array>   \[ (?: (?&value) (?: , (?&value) )* )? (?&ws) \] )
        (?<object>  \{ (?: (?&pair) (?: , (?&pair) )* )? (?&ws) \} )
        (?<value>   (?&ws) (?: (?&number) | (?&boolean) | (?&string) | (?&array) | (?&object) ) (?&ws) )
    )
    \A (?&value) \Z
    /sx
```

P.S. 611 символов - размер регулярки, можно немного ужать, если заменить number на nam, например,  и тд.
Удалить проверку массивов, т.к. не всегда нужно...

---

## 