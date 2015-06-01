# Aggregion.Storage Models

## File

- **resourceId** (`String`) - уникальный идентификатор ресурса. Длина 64 символа из диапазона [a-zA-Z0-9].
- **name** (`String`) - имя файла.
- **path** (`String`) - путь к файлу. Например "images/covers".
- **size** (`Number`) - размер файла в байтах.
- **owner** (`ObjectId`) - владелец (account в storage).
- **checksum** (`String`) - контрольная сумма CRC-32.
- **type** (`String`) - MIME-тип.
- **sharing** (`Object`) - опции шаринга.
    - **byLink** (`Boolean`) - файл доступен всем, у кого есть ссылка.
- **state** (`Object`) - состояние файла.
    - **available** (`Boolean`) - файл доступен для скачивания.
    - **availableBytes** - доступно/загружено в хранилище N первых байт.




### Пример
```javascript
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
```