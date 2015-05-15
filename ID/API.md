FORMAT: 1A
HOST: https://id.aggregion.com/api/

# Aggregion ID
Aggregion ID - сервис авторизации для Aggregion.

# Group Регистрация
Методы для регистрации пользователей.

## Запросы на регистрацию [/reg/request]
Работа с запросами на регистрацию.

Авторизация: не нужна.

### Создать запрос на регистрацию [POST]
+ Response 200 (application/json)

        {
          "id": "1",
          "questionType": "captcha", 
          "question": "http://captachaurl.com/captcha.png",
          "expirationDate": "2019-04-23T18:25:43.511Z"
        }
        
## Регистрация локальных пользователей  [/reg/register]
Авторизация: не нужна.

### Зарегистрировать пользователя [POST]
+ Request (application/json)

        {
          "requestId": "5555fee256d261fe0b642713",
          "answer": "123",
          "user": {
            "info": {
              "email": "ivan1234@gmail.com",
              "firstName": "Ivan",
              "lastName": "Petrov",
              "phoneNumber": "+792712345678",
              "address": "Milky Way galaxy, Solar system, Earth"
            },
            "login": "ivan1234@gmail.com",
            "loginType": "email", 
            "password": "qwerty"
          }
        }

+ Response 201 (application/json)

        { "sessionId" : "ea01b9257c8bc20768709702d90a53a4d43a92f8fb79201023d4a508922a796f" } 


# Group Авторизация
Методы для авторизации пользователей приложений.

## Запрос авторизации локального пользователя [/auth/local]

### Авторизация в ID [POST]
+ Request (application/json)

        {"login": "ivan1234@gmail.com", "password": "qwerty"}

+ Response 200 (application/json)

        { "sessionId" : "afa2e7061ebf65bd5a8193ab1756b977a2a956f067d8c0ae82772d7a020b03f0" } 


## Запрос авторизации пользователя Facebook [/auth/facebook]

### Авторизация [POST]
+ Request (application/json)

        {"id": "0000001", "oauthCode": "12345"}

+ Response 200 (application/json)

        { "sessionId" : "INC60L7QtNC40YDQvtCy0LDQvdC40Y8g0Lg=" } 


## Запрос авторизации пользователя VK [/auth/vk]

### Авторизация [POST]
+ Request (application/json)

        { "oauthCode": "12345" }

+ Response 200 (application/json)

        { "sessionId" : "INC60L7QtNC40YDQvtCy0LDQvdC40Y8g0Lg=" } 


#Group OAuth

## Запрос токена [/oauth/token]
Авторизация: не нужна.

Возможные значения grantType: code, refreshToken;

### Запрос токена для доступа к сервисам [POST]
+ Request (application/json)
    
        {
          "clientId": "12345",
          "clientSecret": "someSecret",
          "grantType" : "code",
          "code": "someCode",
          "refreshToken": null
        }

+ Response 200 (application/json)

        { "token" : "INC60L7QtNC40YDQvtCy0LDQvdC40Y8g0Lg=", "refreshToken" : "ACAA60L7QtNC40YDQvtCy0LDQvdC40Y8g0Lg=" , "expiresIn" : 3600 } 

## Запрос кода [/oauth/code]
Авторизация: нужна.

### Запрос кода для последующего обмена на токен [POST]
+ Request (application/json)
    + Headers
    
            X-Session-Id: INC60L7QtNC40YDQvtCy0LDQvdC40Y8g0Lg=    

    + Body
    
            {
              "clientId": "12345",
              "credentials": {
                "social": ["posts"],
                "distribution": ["subscriptions"]
              }
            }

+ Response 200 (application/json)

        { "code" : "AAABBBCCCDDD=" } 
        

#Group Scope

## Запрос информации и сервисах и scope [/oauth/scopes]
Авторизация: не нужна.

### Получить список сервисов и scope [GET]

+ Response 200 (application/json)

        [{
          "serviceName": "distribution",
          "scopes": [{
                    "title": {
                        "default": "Reading fund",
                        "ru_RU": "Чтение информации о фонде"
                    },
                    "value": "fund.read"
                }]
        }]

## Запрос информации о конкретном сервисе и его scope [/oauth/scopes/{serviceName}]

### Получить информацию о конкретном сервисе и scope [GET]

+ Response 200 (application/json)

        {
          "serviceName": "distribution",
          "scopes": [{
                    "title": {
                        "default": "Reading fund",
                        "ru_RU": "Чтение информации о фонде"
                    },
                    "value": "fund.read"
                }]
        }


#Group Application

## Запрос информации о приложениях [/oauth/applications]
Авторизация: не нужна.

### Получить список приложений [GET]

+ Response 200 (application/json)

        [{
          "clientId": 234,
          "name": "application name"
        }]

## Запрос информации о конкретном приложении [/oauth/applications/{clientId}]

### Получить информацию о конкретном приложении [GET]

+ Response 200 (application/json)

        {
          "clientId": 234,
          "name": "application name"
        }


# Group Users

## Информация о пользователе [/users/me]

### Получить информацию о себе [GET]

+ Response 200 (application/json)

        {
          "info": {
                "email": String,
                "firstName": String,
                "lastName": String,
                "phoneNumber": String,
                "address": String
          },
          "registrationDate": Date
        }

## Информация о аккаунтах [/users/me/accounts]

### Получить информацию о своих аккаунтах [GET]

+ Response 200 (application/json)

        [{
            "owner": 123,
            "name": "Школа №1",
            "admins": [123, 456]
        }]


### Добавить аккаунт [POST]

## Информация о конкретном аккаунте [/users/me/accounts/{id}]

### Получить информацию о конкретном аккаунте [GET]

### Изменить аккаунт [PATCH]

Поля, доступные для изменения: name, admins, isOrganization, organizationDetails.


# Group Groups

## Список групп [/groups]

Доступные поля для filter:

    - name
    - parent
    - member

Доступные поля для extend:

    - members

### Получить список групп [GET]

+ Response 200 (application/json)

        [$Group]


### Добавить группу [POST]

+ Request (application/json)

        $Group

+ Response 201 (application/json)

        $Group

## Конкретная группа [/groups/{id}]

### Получить группу [GET]

+ Response 200 (application/json)

        $Group

### Изменить группу [PATCH]

Возможные поля для изменения: name, members, parent.

### Удалить группу [DELETE]

+ Response 204

## Группы в виде дерева [/groups/tree]

### Получить группы в виде дерева [GET]

Дочерние группы добавляются в поле children.

+ Response 200 (application/json)

        [$Group]


# Group Public

## Пользователи [/public/users]

### Получить список пользователей [GET]

Возможные поля для filter:

    - nickname
    - info.firstName
    - info.lastName

Возвращаемые поля:

    - id
    - nickname
    - info.firstName
    - info.lastName

Должен поддерживаться параметр textsearch.

Запрос списка без filter или textsearch запрещен.

+ Response 200 (application/json)

        [$User]

## Конкретный пользователь [/public/users/{id}]

### Получить конкретного пользователя [GET]

+ Response 200 (application/json)

        $User

## Аккаунты [/public/accounts]

### Получить список аккаунтов [GET]

Возвращаемые поля:

    - id
    - name
    - isOrganization
    - organizationDetails

Возможные поля для filter:

    - name
    - isOrganization
    - organizationDetails.inn

Должен поддерживаться параметр textsearch.

Запрос списка без filter или textsearch запрещен.

+ Response 200 (application/json)

        [$Account]