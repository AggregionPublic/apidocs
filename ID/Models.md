# User

Пользователь

- **nickname** (`String`, `unique`) - никнейм (генерируется автоматически).
- **info** (`Object`) - информация о пользователе.
	- **email** (`String`) - электронная почта.
	- **firstName** (`String`) - имя.
	- **lastName** (`String`) - фамилия.
	- **phoneNumber** (`String`) - телефонный номер.
	- **address** (`String`) - адрес.
- **registrationDate** (`Date`) - дата регистрации


# Account

Аккаунт пользователя или организации.

- **owner** (`ObjectId`, `ref: 'User'`) - владелец.
- **name** (`String`) - название.
- **admins** (`[ObjectId]`) - список администраторов аккаунта.
- **options** (`[Object]`) - дополнительные поля для внешних сервисов.
- **isOrganization** (`Boolean`, `required`) - является ли аккаунт аккаунтом организации.
- **organizationDetails** (`Object`) - реквизиты организации
	- **address** (`String`) - адрес.
	- **legalAddress** (`String`) - юридический адрес.
	- **inn** (`String`) - ИНН.
	- **kpp** (`String`) - КПП.
	- **bankName** (`String`) - название банка.
	- **bankCity** (`String`) - город банка.
	- **bik** (`String`) - БИК.
	- **corrAccount** (`String`) - корреспондентский счет.
	- **account** (`String`) - счет.
	- **tel** (`String`) - телефон.
	- **accountant** (`String`) - бухгалтер.
	- **director** (`String`) - директор.

# Service 

Сервис Aggregion

- **name** (`String`) - название сервиса.
- **scopeValues** (`Object`) - допустимые значения области видимости:
	- **title** (`Object`) - название на разных языках.
		- **default** - значение по умолчанию.
		- **ru_RU** - значение для русского языка.
	- **value** (`String`) - значение.

# Application

Внешнее приложение

- **name** (`String`) - название приложения.
- **clientId** (`String`) - id приложения.
- **clientSecret** (`String`) - секрет приложения. 

## Пример
```javascript
{
	"name": String,
	"clientId": String,
	"clientSecret": String
}
```

# Token

Токен авторизации в сервисах

- **user** (`ObjectId`) - пользователь, которому выдан токен.
- **application** (`ObjectId`) - приложение, которое запросило токен.
- **service** (`ObjectId`) - cервис, к которому запросили доступ.
- **scope** (`[String]`) - сбласть видимости для которой запрошен доступ в сервисе.
- **creationDate** (`Date`) - дата создания.
- **expirationDate** (`Date`) - дата протухания.,
- **refreshToken** (`String`) - код обновления токена.
- **refreshTokenExpirationDate** (`Date`) - дата протухания кода обновления. 

## Пример

```javascript
{
	"user": ObjectId,
	"application": ObjectId,
	"service": ObjectId,
	"scope": [String],
	"creationDate": Date,
	"expirationDate": Date,
	"refreshToken": String,
	"refreshTokenExpirationDate": Date,
}
```

# RegistrationRequest

Запрос на регистрацию

- **questionType** (`String`) - тип вопроса: "none", "captcha".
- **question** (`String`) - вопрос или URL, в зависимости от типа.
- **answer** (`String`) - ответ на вопрос.
- **expirationDate** (`Date`) - время протухания. 

## Пример

```javascript
{
	"questionType": String,
	"question": String,
	"answer": String,
	"expirationDate": Date
}
```

# Session

Сессия пользователя в ID

- **sessionId** (`String`) - ID сессиию
- **user** (`ObjectId`) - пользователь, которому выдан ID сессиию
- **expirationDate** (`Date`) - дата истечения сессиию


## Пример

```javascript
{
	"sessionId": String,
    "user": ObjectId,
    "expirationDate": Date
}
```

# Group

Группа

- **owner** (`ObjectId`, `required`, `ref: 'Account'`) - владелец.
- **name** (`String`, `required`) - название группы
- **parent** (`ObjectId`, `ref: 'Group'`) - родительский элемент.
- **members** (`[ObjectId]`, `ref: 'User'`) - члены группы.



