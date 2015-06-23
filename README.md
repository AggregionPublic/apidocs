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

# Описание работы текстового поиска
textsearch=value
Ищет совпадения по тексту сразу по нескльким полям модели

Пример:
```
url?textsearch=пушкин
```

# Описание работы раскрытия полей (extend)
Если поле в модели ссылается на сущность другой модели, то можно его раскрыть и превратить в объект.

Пример:

http://ds.aggregion.dev.e-azbuka.corp/api/public/catalog
```
[
  {
    "description": {"default": "2+2", "ru_RU": "2+2"},
    "owner": "5555ba3fb01666bd2a0de5fc",
    "title": {"default": "C++ Forever", "ru_RU": "Язык программирования C++"}
  }
]
```

http://ds.aggregion.dev.e-azbuka.corp/api/public/catalog?extend=owner
```
[
  {
    "description": {"default": "2+2", "ru_RU": "2+2"},
    "owner": {"name": "Ivan Ivanov", "isOrganization": false, "id": "5555ba3fb01666bd2a0de5fc"},
    "title": {"default": "C++ Forever", "ru_RU": "Язык программирования C++"}
  }
]
```
