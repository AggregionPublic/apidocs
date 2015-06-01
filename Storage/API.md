FORMAT: 1A

HOST: https://storage.aggregion.com/api/

# Aggregion Storage
Aggregion Storage - сервис облачного хранилища для Aggregion.

Все действия, кроме получения ссылок на файлы, производятся от имени пользователя и аккаунта. Авторизация обязательна. Пользователю доступны для управления только файлы, принадлежащие доступным ему аккаунтам.

Заголовок для передачи аккаунта: X-Account.

Пример:


		X-Account: 12345678

# Group Files

## Управление файлами [/files]

### Загрузить файл [POST]

+ Request (multipart/form-data, boundary=SomeGenetatedBoundary)

	+ Headers

			Content-Length: {Общая длина тела}

	+ Body

			--SomeGenetatedBoundary
			content-disposition: form-data; name="meta"
			Content-Type: application/json

			{"name": "Gold Prelim eText Coursebook.azbuka", "sharing": {
			  "byLink": true
			}, "path": "/"}


+ Response 201 (application/json)

			{  
			      "checksum":"907044547",
			      "type":"application/x-azbuka-zipbundle",
			      "size":81972725,
			      "resourceId":"3b3749b34489fff42ade17ed8adfb9d14e188ba7d74e4431af69fc92e8a5b5c2",
			      "name":"Gold Prelim eText Coursebook.azbuka",
			      "owner":"556c3c356d7513113e60a336",
			      "state":{  
			         "available":true,
			         "availableBytes":81972725
			      },
			      "sharing":{  
			         "byLink":true
			      },
			      "path":"/"
			}


### Получить список файлов [GET]

+ Response 200 (application/json)

			[{  
			      "checksum":"907044547",
			      "type":"application/x-azbuka-zipbundle",
			      "size":81972725,
			      "resourceId":"3b3749b34489fff42ade17ed8adfb9d14e188ba7d74e4431af69fc92e8a5b5c2",
			      "name":"Gold Prelim eText Coursebook.azbuka",
			      "owner":"556c3c356d7513113e60a336",
			      "state":{  
			         "available":true,
			         "availableBytes":81972725
			      },
			      "sharing":{  
			         "byLink":true
			      },
			      "path":"/"
			}]


## Работа с конкретным файлом [/files/{id}]

### Получить информацию о файле [GET]

+ Response 200 (application/json)

			{
			    "resourceId": "dkshdiueiuweyiurui432435hjfkdh3dfsd"
			    "name": "My file",
			    "size": 500000,
			    "owner": 12345,
			    "checksum": "crc32",
			    "type": "mime/type"
			    "sharing": {
			        "byLink": true
			    },
			    "state": {
			        "available": true,
			        "availableBytes": 500000
			    }
			}

### Изменить информацию о файле [PATCH]

Доступные для изменения поля:
- name;
- sharing;
- path;

+ Request (application/json)

			{"name": "New name", "sharing": {
			  "byLink": false
			}, "path": "new/path"}



+ Response 200 (application/json)

			{
			    "resourceId": "dkshdiueiuweyiurui432435hjfkdh3dfsd"
			    "name": "New name",
			    "size": 500000,
			    "owner": 12345,
			    "checksum": "crc32",
			    "type": "mime/type"
			    "sharing": {
			        "byLink": false
			    },
			    "path": "new/path",
			    "state": {
			        "available": true,
			        "availableBytes": 500000
			    }
			}


### Удалить файл [DELETE]

+ Response 204

## Получение ссылки на скачивание файла [/files/{id}/shared/data]

Без авторизации.

### Редирект [GET]

+ Response 301

	+ Headers

            Cache-Control: no-cache
			Location: http://dl25.aggregion.com/dkshdiueiuweyiurui432435hjfkdh3dfsd

## Получение ссылки на скачивание торрент-файла [/files/{id}/shared/torrent]

Без авторизации.

### Данные [GET]

+ Response 200 (application/x-bittorrent)


			binaryData


## Получение ссылки на скачивание файла [/files/{id}/data]


### Редирект [GET]

+ Response 301

	+ Headers

            Cache-Control: no-cache
			Location: http://dl25.aggregion.com/dkshdiueiuweyiurui432435hjfkdh3dfsd

## Получение ссылки на скачивание торрент-файла [/files/{id}/torrent]


### Данные [GET]

+ Response 200 (application/x-bittorrent)


			binaryData