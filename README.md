Описание API платформы Aggregion.

# Сервис ID

- [API](ID/API.md)
- [Models](ID/Models.md)

# Сервис Distribution

- [API](Distribution/API.md)
- [Models](Distribution/Models.md)

# Сервис Market

- [API](Market/API.md)
- [Models](Market/Models.md)

# Сервис Storage

- [API](Storage/API.md)
- [Models](Storage/Models.md)

# Описание работы фильтров
```
filter=field(value, sign)
value = "String" | bool | json array (["val1", "val2"])
sign = equals, greater, less, notequals, regex, in
```

Примеры:
```
url?filter=field("value",equals)          // Найдёт все записи у которых field = "value"
url?filter=field(true,equals)             // Найдёт все записи у которых field = true
url?filter=field("3",greater)             // Найдёт все записи у которых field > 3
url?filter=field("5",less)                // Найдёт все записи у которых field < 5
url?filter=field("value",notequals)       // Найдёт все записи у которых field != "value"
url?filter=field("pattern",regex)         // Найдёт все записи у которых field подходит по паттерну регулярного выражения
url?filter=field(["value1","value2"],in)  // Эквивалентно оператору IN в SQL
```
