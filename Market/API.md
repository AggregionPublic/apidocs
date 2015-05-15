FORMAT: 1A
HOST: https://market.aggregion.com/api/

# Group Showcase

Витрина.

## Управление витринами [/showcase]

### Получить список витрин [GET]

Возможные поля для extend:

	- owner

Возможные поля для filter:

	- owner
	- name


Возможные поля для order:

	- name


Возможные поля для textsearch:

	- name

+ Response 200 (application/json)


			[$Showcase]

### Добавить витрину [POST]

+ Response 201 (application/json)


			$Showcase


## Управление конкретной витриной [/showcase/{id}]

### Добавить витрину [PATCH]

Доступные для изменения поля:

	- name
	- status

# Group Goods

Позиции витрины.

## Управление позициями витрины [/goods]

Доступны только позиции, где текущий аккаунт является владельцем.

### Получить список позиций витрины [GET]

Возможные поля для extend:

	- owner

Возможные поля для filter:

	- owner
	- showcase
	- catalog
	- licensePeriod
	- cost
	- currency
	- status

Возможные поля для order:

	- cost


+ Response 200 (application/json)


			[$Good]

### Добавить позицию витрины [POST]

Добавить позицию витрины можно в одном из следующих случаев:

	- owner позиции каталога является текущий аккаунт
	- указан parent и текущий аккаунтом является дилером для этой позиции


+ Response 201 (application/json)


			$Good

## Управление конкретной позицией [/goods/{id}]

### Изменить позицию [PATCH]

Доступные для изменения поля: 

- showcase
- cost
- status

В случае изменения cost или status, изменяется статус для всех документов на changed, где в качестве parent указана текущая позиция (рекурсивно).



# Group Orders

## Список заказов [/orders]

Возвращается список заказов, в котором текущий аккаунт - исполнитель.

### Получить список заказов [GET]

+ Response 200 (application/json)


			[$Order]

### Создать заказ [POST]

При создании заказа исполнителем и владельцем является текущий аккаунт.

+ Request (application/json)

			{"contragent" : "123", "showcase": "456"}

+ Response 201 (application/json)


			$Order

## Конкретный заказ [/orders/{id}]

### Получить конкретный заказ [GET]

+ Response 200 (application/json)


			$Order


### Изменить заказ [PATCH]

Возможные для изменения поля: contragent, showcase

+ Response 200 (application/json)


			$Order

### Удалить заказ [DELETE]

Удалить можно заказы только со статусом `new`.

+ Response 204


## Позиции заказа [/orders/{id}/items]

Редактировать позиции можно только для заказа со статусом new.

### Получить список позиций заказа [GET]

### Добавить позицию заказа [POST]

Позиция создается только с указанием позиции витрины и количества. Осуществляется проверка, что позиция витрины принадлежит текущему аккаунту. Если в заказе уже есть позиция с переданным good.id, то вместо новой позиции, в существующую добавляется переданное количество.

+ Request (application/json)

			
			{
				"good": "good.id",
				"qty": 10
			}

+ Response 201 (application/json)

			$OrderItem

### Удалить позицию заказа [DELETE]

## Отмена заказа [/orders/{id}/cancel]

### Отменить заказ [POST]

Статус изменяется на `cancelled`. Можно отменить только заказ со статусом `new`.

## Подтверждение заказа [/orders/{id}/accept]

### Подтвердить заказ [POST]

Статус изменяется на `accepted`. Можно отменить только заказ со статусом `new`.

При подтверждении заказа создаются экземпляры (Item) в фонде по умолчанию заказчика:

	- creator - владелец продаваемой позиции каталога
	- owner - заказчик
	- catalog - позиция каталога
	- fund - фонд по умолчанию заказчика
	- creationDate - текущая дата
	- expirationDate - текущая дата + период лицензии

Создается документ с типом order и статусом accepted и на основе него создается транзакция (Transaction). В поле options документа создается  опция order со значением id заказа. В качестве oldFund в транзакции указывается фонд по умолчанию исполнителя.



# Group Dealer

Возможные поля для extend:

	- owner

Возможные поля для filter:

	- owner
	- showcase
	- catalog
	- licensePeriod
	- cost
	- currency
	- status

Возможные поля для order:

	- cost

## Список позиций, доступный дилеру [/dealer/goods]

## Получить список позиций, доступный дилеру [GET]

Ответ содержит все позиции со статусами changed или sale, где текущий аккаунт является дилером (находится в списке dealers).

+ Response 200 (application/json)


			[$Good]


# Group Public

## Список витрин [/public/showcases]

### Получить список витрин [GET]

+ Response 200 (application/json)


			[$Showcase]


## Информация о витрине [/public/showcases/{id}]

### Получить информацию о витрине [GET]

Возможные поля для extend:

	- owner

+ Response 200 (application/json)


			$Showcase


## Список товаров [/public/goods]

Возвращаются элементы со статусом sale.

Возможные поля для extend:

	- owner
	- showcase

Возможные поля для filter:

	- owner
	- showcase
	- catalog
	- licensePeriod
	- cost
	- currency
	- status

Возможные поля для order:

	- cost

Возможные поля для group:

	- showcase
	- catalog


+ Response 200 (application/json)


			[$Good]


## Заказы [/public/orders]

### Получить список заказов [GET]

Возвращаются все элементы, где текущий аккаунт является контрагентом.

Возможные поля для extend:

	- owner
	- contragent

Возможные поля для filter:

	- owner
	- number
	- date

Возможные поля для order:

	- number
	- date

+ Response 200 (application/json)


			[$Order]


### Создать заказ [POST]

Осуществляется проверка, что good.status == 'sale'.

+ Request (application/json)


			{	
				"showcase": "123",
				"goods": 
					[{
						"good": "good.id",
						"qty": 10
					}, {
						"good": "good.id",
						"qty": 20
					}]
			}

+ Response 201 (application/json)

			$Order


## Конкретный заказ [/public/orders/{id}]

### Получить конкретный заказ [GET]

Возможные поля для extend:

	- owner
	- contragent


## Отмена заказа [/public/orders/{id}/cancel]

### Отменить заказ [POST]

+ Response 201 (application/json)

			$Order


## Получить ссылку на оплату заказа [/public/orders/{id}/buyUrl]

### Получить ссылку на оплату заказа [GET]

Возвращается ссылка на оплату заказа с подставленными значениями showcase и order. Если для showcase не указан шаблон buyUrl, то возвращается 404.

+ Response 201 (application/json)

			$Order
