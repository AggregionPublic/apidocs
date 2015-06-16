FORMAT: 1A
HOST: https://ds.aggregion.com/api/

# Aggregion Distribution
Aggregion DS - сервис дистрибуции для Aggregion.

Все действия производятся от имени пользователя и аккаунта. Авторизация обязательна. Пользователю доступны для управления только файлы, принадлежащие доступным ему аккаунтам.

Заголовок для передачи аккаунта: X-Account.

Пример:

		X-Account: 12345678

# Group Catalog

Возможные поля для extend:

	- owner

Возможные поля для filter:

	- title.{lang}
	- description.{lang}
	- tags
	- platformSupport
	- options.key && options.value

Возможные поля для order:

	- title.{lang}

Запрещенные для редактирования поля:

	- isPublic (пока нет модерации - владелец позиции может изменять это свойство)
	- publishingStatus (владельцу позиции можно установить только статус 'none' и 'published' позже, когда появится модерация - набор доступных статусов будет другим)
	- rejectReason 

## Управление каталогом [/catalog]

### Получить список позиций каталога [GET]

Должен поддеживать Range.

+ Response 200 (application/json)

			
			[{
				"id": "123",
                "owner": "123",
                "title": {
                    "default": "English",
                    "ru_RU": "Название на русском языке"
                },
                "description": {
                    "default": "English",
                    "ru_RU": "Описание на русском языке"
                },
                "cover": "cover_url",
                "tags": ["String"],
                "platformSupport": [
                    "windows",
                    "ios",
                    "android",
                    "android4.3+"
                ],
                "previewImages": [
                    "url",
                    "url"
                ],
                "previewVideos": [
                    "url",
                    "url"
                ],
                "options": {
                    "language": "ru_RU",
                    "isbn": "isbn",
                    "someOption": "someValue"
                }
			}]



### Добавить позицию каталога [POST]

+ Request (application/json)


			{
			    "title": {
			        "default": "English",
			        "ru_RU": "Название на русском языке"
			    },
			    "description": {
			        "default": "English",
			        "ru_RU": "Описание на русском языке"
			    },
			    "cover": "cover_url",
			    "tags": ["String"],
			    "platformSupport": [
			        "windows",
			        "ios",
			        "android",
			        "android4.3+"
			    ],
			    "previewImages": [
			        "url",
			        "url"
			    ],
			    "previewVideos": [
			        "url",
			        "url"
			    ],
			    "options": {
			        "language": "ru_RU",
			        "isbn": "isbn",
			        "someOption": "someValue"
			    }
			}


+ Response 201 (application/json)

			
			{
				"id": "123",
                "owner": "123",
                "title": {
                    "default": "English",
                    "ru_RU": "Название на русском языке"
                },
                "description": {
                    "default": "English",
                    "ru_RU": "Описание на русском языке"
                },
                "cover": "cover_url",
                "tags": ["String"],
                "platformSupport": [
                    "windows",
                    "ios",
                    "android",
                    "android4.3+"
                ],
                "previewImages": [
                    "url",
                    "url"
                ],
                "previewVideos": [
                    "url",
                    "url"
                ],
                "options": {
                    "language": "ru_RU",
                    "isbn": "isbn",
                    "someOption": "someValue"
                }
			}


## Управление позицией каталога [/catalog/{id}]

### Получить конкретную позицию [GET]

+ Response 200 (application/json)

			
			{
				"id": "123",
                "owner": "123",
                "title": {
                    "default": "English",
                    "ru_RU": "Название на русском языке"
                },
                "description": {
                    "default": "English",
                    "ru_RU": "Описание на русском языке"
                },
                "cover": "cover_url",
                "tags": ["String"],
                "platformSupport": [
                    "windows",
                    "ios",
                    "android",
                    "android4.3+"
                ],
                "previewImages": [
                    "url",
                    "url"
                ],
                "previewVideos": [
                    "url",
                    "url"
                ],
                "options": {
                    "language": "ru_RU",
                    "isbn": "isbn",
                    "someOption": "someValue"
                }
			}


### Изменить конкретную позицию [PATCH]

+ Request (application/json)


			{
			    "title": {
			        "default": "New title",
			        "ru_RU": "Новое название"
			    }
			}


+ Response 201 (application/json)

			
			{
				"id": "123",
                "owner": "123",
                "title": {
                    "default": "New title",
                    "ru_RU": "Новое название"
                },
                "description": {
                    "default": "English",
                    "ru_RU": "Описание на русском языке"
                },
                "cover": "cover_url",
                "tags": ["String"],
                "platformSupport": [
                    "windows",
                    "ios",
                    "android",
                    "android4.3+"
                ],
                "previewImages": [
                    "url",
                    "url"
                ],
                "previewVideos": [
                    "url",
                    "url"
                ],
                "options": {
                    "language": "ru_RU",
                    "isbn": "isbn",
                    "someOption": "someValue"
                }
			}


### Удалить позицию каталога [DELETE]

Удалить можно только ту позицию, для которой не создан ни один item.

+ Response 204

## Публикация позиции [/catalog/{id}/publish]

### Подать запрос на публикацию [POST]

Запрос без тела.

+ Request


+ Response 200 (application/json)

		$Catalog


## Снятие с публикации [/catalog/{id}/unpublish]

### Снять публикации [POST]

Запрос без тела.

+ Request


+ Response 200 (application/json)

		$Catalog




# Group Bundle

## Управление списком бандлов [/bundles]

Возможные поля для extend:

	- owner
	- catalog

Возможные поля для filter:

	- owner
	- catalog
	- resourceId

### Получить список бандлов [GET]

+ Response 200 (application/json)


			[{
			    "id": "001",
			    "owner": "123",
			    "version": "1.0",
			    "resourceId": "123",
			    "catalog": "456"
			}]
            
            


### Добавить бандл [POST]



+ Request (application/json)

			{
			    "owner": "123",
			    "version": "1.0",
			    "catalog": "456",
			    "sourceResourceId": "123"
			}


+ Response 201 (application/json)

			{
				"id": "456",
                "owner": "123",
                "version": "1.0",
                "resourceId": "123",
                "catalog": "456",
                "available": false
			}


## Управление конкретным бандлом [/bundles/{id}]

### Получить информацию о бандле [GET]

+ Response 200

			{
				"id": "456",
			    "owner": "123",
			    "version": "1.0",
			    "resourceId": "123",
			    "catalog": "456",
			    "available": false
			}


### Удалить бандл [DELETE]

+ Response 204



# Group Fund

Возможные поля для extend:

	- owner
	- items (присоединяются экземпляры, относящиеся к данному фонду)

Возможные поля для filter:

	- owner
	- name


Возможные поля для order:

	- name

## Управление списком фондов [/funds]

### Получить список фондов [GET]

+ Response 200 (application/json)

			
			[{
				"id": "456",
                "owner": "123",
                "name": "Название фонда"
			}]


### Добавить фонд [POST]

+ Request (application/json)

			{
			    "owner": "123",
			    "name": "Название фонда"
			}

+ Response 200 (application/json)

			
			{
				"id": "456",
                "owner": "123",
                "name": "Название фонда"
			 }


## Управление конкретным фондом [/funds/{id}]

### Получить фонд [GET]

+ Response 200 (application/json)

			
			{
				"id": "456",
                "owner": "123",
                "name": "Название фонда"
			}


### Изменить фонд [PATCH]

Возможные поля для изменения:

	- name

+ Request (application/json)

			{ "name": "Новое название" }


+ Response 200 (application/json)

			
			{
				"id": "456",
                "owner": "123",
                "name": "Новое название"
			}


### Удалить фонд [DELETE]

Нельзя удалять фонд по умолчанию. При удалении остальных фондов, все связанные с ним экземпляры переносятся в фонд по умолчанию. При этом создается транзакция с типом "displacement".

+ Response 204


## Получить сгруппированные позиции фонда [/funds/{id}/grouped]

Возможные поля для extend:

    - catalog

### Получить фонд [GET]

+ Response 206 (application/json)

    		
			[{
				"catalog": "553a434e41a76a260efc00ef",
		        "items": [{
                    "creationDate": "2015-04-24T13:21:18.000Z",
                    "expirationDate": "2015-05-04T13:21:18.000Z",
                    "qty": 9
                }]
			}]


# Group Items


Возможные поля для extend:

	- catalog
	- fund
	- lease (активный лиз для экземпляра) 

Возможные поля для filter:

	- catalog
	- fund
	- creationDate
	- expirationDate

Возможные поля для filter/order:

	- creationDate
	- expirationDate


## Управление списком экземпляров [/items]


### Получить список экземпляров [GET]


+ Response 200 (application/json)


			[{
                "catalog": "ObjectId",
                "fund": "ObjectId",
                "creationDate": "Date",
                "expirationDate": "Date"
			}]


### Добавить экземпляр [POST]

Разрешается добавлять экземпляр только для своей позиции каталога.

+ Request (application/json)


			{
                "catalog": "ObjectId",
                "fund": "ObjectId",
                "expirationDate": "Date"
			}


+ Response 201 (application/json)



			{
                "creator": 123,
                "owner": "123",
                "catalog": "ObjectId",
                "fund": "ObjectId",
                "creationDate": "Date",
                "expirationDate": "Date"
			}


## Массовые операции с экземплярами [/items/multi]

### Добавить экземпляр [POST]

Разрешается добавлять экземпляр только для своей позиции каталога.

+ Request (application/json)


			{
                "catalog": "ObjectId",
                "fund": "ObjectId",
                "expirationDate": "Date",
                "qty": Number
			}


+ Response 201 (application/json)



			[{
                "creator": 123,
                "owner": "123",
                "catalog": "ObjectId",
                "fund": "ObjectId",
                "creationDate": "Date",
                "expirationDate": "Date"
			}]


## Передать экземпляры во владение другому аккаунту [/items/moveToAccount]

### [POST]

Автоматически создается документ с типом invoice и с указанными опциями и транзакция.

+ Request (application/json)
			
			{
				"items": [
					{
						"catalog": "123",
						"expirationDate": "date",
						"qty": 1
					},
					{
						"catalog": "456",
						"expirationDate": "date",
						"qty": 2
					}
				],
				"account": "accountId",
				"documentOptions": {}
			}

+ Response 201


## Передать экземпляры в другой фонд [/items/moveToFund]

### [POST]

Разрешается передача только в фонд, владельцем которого является текущий аккаунт. Автоматически создается транзакция.

+ Request (application/json)
			
			{
				"items": [
					{
						"catalog": "123",
						"expirationDate": "date",
						"qty": 1
					},
					{
						"catalog": "456",
						"expirationDate": "date",
						"qty": 2
					}
				],
				"fund": "fundId"
			}

+ Response 201
			

# Group Documents

## Управление список документов [/documents]

Возможные поля для extend:

	- owner
	- contragent
	- squad.catalog

Возможные поля для filter/order:

	- owner
	- contragent
	- options.key && options.value
	- squad.catalog
	- status


### Получить список документов [GET]

Получить можно те документы, где аккаунт является владельцем или контрагентом.

### Создать документ [POST]

+ Request (application/json)


			{"contragent": "123", "type": "invoice", "squad": ["catalog": "123", "qty": 10, "licensePeriod": 365]}
			
+ Response 201 (application/json)


			$Document

## Управление конкретным документом [/documents/{id}]

### Получить документ [GET]

Получить можно те документы, где аккаунт является владельцем или контрагентом.

### Удалить документ [DELETE]

Удалить можно только те документы, где ты владелец. Нельзя удалять документ, если на него ссылается хотя бы одна транзакция.

### Изменить документ [PATCH]

Изменить можно только те документы, где ты владелец.

Возможные поля для изменения:

	- contragent
	- options
	- squad
	- refDoc
	- status


# Group Transactions

## Управление списком транзакций [/transactions]

Возможные поля для extend:

	- sender
	- receiver
	- document
	- oldFund
	- newFund
	- items

Возможные поля для filter:

	- sender
	- receiver
	- document
	- date
	- oldFund
	- newFund
	- items (по id)

Возможные поля для order:

	- date

Аккаунту доступны транзакции, где он receiver или sender.


### Получить список транзакций [GET]

Аккаунту доступны транзакции, где он receiver или sender.

### Создать транзакцию [POST]

При создании транзакции все указанные экзмепляры перемещаются из oldFund в newFund, кроме случая, когда oldFund пустой.
Также owner у экземпляров меняется на receiver.

# Group Leases

## Управление списком лизов [/leases]

Возможные поля для extend:

	- item
	- item.fund
	- item.catalog
	- user
	- keys


Возможные поля для filter:

	- item
	- user
	- keys
	- beginDate 
	- expirationDate 

Возможные поля для order:

	- creationDate
	- expirationDate

### Получить список лизов [GET]

### Создать лиз [POST]

Создать лиз можно только на item, в котором текущий аккаунт - owner и даты создаваемого лиза не должны пересекаться с существующими.
Поле maxKeys должно быть установлено таким же, какое оно на данный момент в позиции каталога, к которой относится item.

### Изменить лиз [PATCH]

Доступные для изменения поля:

	- isActive (только из true в false, но не обратно)

## Конкретный лиз [/leases/{id}]

### Получить конкретный лиз [GET]


# Group Public

## Публичный каталог [/public/catalog]

Возможен доступ без авторизации.

Возможные поля для extend:

	- owner


Возможные поля для filter:

	- title
	- description 

### Получить список позиций каталога [GET]

Должны выдаваться позиции с isPublic = true.

## Публичный каталог, конкретная позиция [/public/catalog/{id}]

### Получить конкретную позицию каталога [GET]

## Публичный каталог, бандлы конкретной позиции [/public/catalog/{id}/bundles]

### Получить список бандлов конкретной позиции каталога [GET]

## Публичный каталог, бандл [/public/catalog/{id}/bundles/{bundleId}]

### Получить конкретный бандл [GET]

## Сигнатура бандла [/public/catalog/{id}/bundles/{bundleId}/signature]

### Сгенерировать сигнатуру бандла [POST]

Должна быть сгенерирована сигнатура и помещена в хранилище владельца бандла (в папку .signatures).
Название файла сигнатуры в хранилище = bundle.id + key.sn

+ Request (application/json)

	
			{"keyNumber": "123", "license": "some_base64"}

+ Response 200 (application/json)


			{"resourceId": "456"}




# Group Client

Доступ с авторизацией и с контекстом аккаунта.

## Список лизов [/client/leases]

Возвращаются только активные лизы (как по признаку активности, так и по дате).

Возможные поля для extend:

	- owner
	- item
	- item.catalog
	- item.fund


### Получить список лизов [GET]

## Конкретный лиз [/client/leases/{id}]

### Получить конкретный лиз [GET]

## Привязка лиза [/client/leases/{id}/bind]

### Привязать лиз [POST]

Возможна привязка лиза только к существующему ключу.


+ Request (application/json)

	
			{"keyNumber": "123"}

+ Response 200 (application/json)


			$Lease


## Отвязать лиз [/client/leases/{id}/unbind]

### Отвязать лиз  [POST]

Из cписка ключей лиза должен быть удален ключ.

+ Request (application/json)

	
			{"keyNumber": "123"}


+ Response 200 (application/json)


			$Lease


## Сгенерировать лицензию [/client/leases/{id}/license]

### Сгенерировать лицензию [POST]

Лицензия помещается в хранилище владельца лиза.

+ Request (application/json)

	
			{"keyNumber": "123"}


+ Response 201 (application/json)


			{"resourceId": "123"}


## Список ключей [/client/keys]

Доступен список ключей, где ты user.

### Создать ключ [POST]

Номер генерируется автоматически. Тело записывается в хранилище.

+ Request (application/json)


			{"deviceId": "qqwweedfsd", "deviceName": "Мой планшет"}


+ Response 201 (application/json)


			$Key

### Изменить ключ [PATCH]

Возможные для изменения поля: deviceName.
