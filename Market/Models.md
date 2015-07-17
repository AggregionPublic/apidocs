# Showcase

Витрина

- **owner** (`ObjectId`, `required`, `ref: 'Account'`) - владелец.
- **name** (`String`, `required`) - название витрины.
- **buyUrl** (`String`) - ссылка для оплаты заказа витрины с плейсхолдерами {showcase}, {order} в местах, куда должны быть вставлены id витрины и заказа, соответственно.
- **type** (`String`, `required`, `enum: ['user', 'organization', 'all']`) - тип витрины:
	- user - для пользователей.
	- organization - для организаций.
	- all - для всех.
- **status** (`String`, `required`, `enum: ['archived', disabled', 'changed', 'sale']`) - статус:
	- archived - витрина в архиве.
	- disabled - витрины не выставлена на продажу.
	- sale - витрина выставлена на продажу.



# Good

Продаваемая позиция

- **owner** (`ObjectId`, `required`, `ref: 'Account'`) - владелец.
- **showcase** (`ObjectId`, `ref: 'Showcase'`) - витрина.
- **parent** (`ObjectId`, `ref: 'Good'`) - родительская позиция.
- **catalog** (`ObjectId`, `required`, `ref: 'Catalog'`) - позиция каталога, которая выставлена на продажу.
- **licensePeriod** (`Number`) - период лицензии в днях. Если не указан, то период бесконечен.
- **cost** (`Number`, `required`) - цена.
- **currency** (`String`, `enum: ['RUR', 'USD', 'GBP', 'EUR']`, `required`) - валюта.
- **dealers** (`ObjectId`, `ref: 'Account'`) - список дилеров позиции.
- **status** (`String`, `required`, `enum: ['archived', disabled', 'changed', 'sale']`) - статус:
	- archived - позиция витрины в архиве.
	- disabled - позиция витрины не продается.
	- changed - позиция витрины не продается, существуют изменения в родительской позиции.
	- sale - позиция витрины продается.


# Order

Заказ.

- **owner** (`ObjectId`, `required`, `ref: 'Account'`) - - владелец/исполнитель (showcase.owner).
- **number** (`String`, `required`) - автоинкрементируемое поле номера заказа.
- **contragent** (`ObjectId`, `required`, `ref: 'Account'`) - контрагент (заказчик).
- **showcase** (`ObjectId`, `required`, `ref: 'Showcase'`) - витрина.
- **date** (`Date`, `required`) - дата заказа.
- **status** (`String`, `required`, `enum: ['new', 'accepted', 'cancelled']`) - статус заказа.

# OrderItem

Позиция заказа.

- **owner** (`ObjectId`, `required`, `ref: 'Account'`) - владелец/исполнитель (good.owner).
- **order** (`ObjectId`, `required`, `ref: 'Order'`) - заказ, которому принадлежит позиция.
- **baseCost** (`Number`) - базовая цена (good.parent.cost).
- **cost** (`Number`, `required`) - цена продажи (good.cost).
- **currency** (`String`, `enum: ['RUR', 'USD', 'GBP', 'EUR']`, `required`) - валюта.
- **catalog** (`ObjectId`, `required`, `ref: 'Catalog'`) - позиция каталога.
- **licensePeriod** (`Number`) - период лицензии в днях. Если не указан, то период бесконечен.
- **good** (`ObjectId`, `required`, `ref: 'Good'`) - позиция витрины, которая была продана.
- **qty** (`Number`, `required`) - количество.
- **dealer** (`ObjectId`, `ref: 'Account'`) - дилер (good.parent.owner).
- **dealersChain** (`ObjectId`, `ref: 'Account'`) - цепочка дилеров (good.parent.owner рекурсивно для всех parent). От владельца к конечному исполнителю.













