Создание пользовательских полей
===============================


Контур КЭДО позволяет добавлять пользовательские поля в основные сущности системы: 

* Пользователя (User) 
* Документы (Documents)


Создание пользовательских через API
-----------------------------------

Для того, чтобы добавить пользовательское поле в сущность, необходимо объявить его в настройках (Settings) рабочего пространства (Workspace).

Метод API:

.. code-block:: 

    PATCH https://crm.kontur.ru/api/v1/{ws}/settings


В модели Settings есть поле CustomFields, в котом описываются пользовательские поля.

*Примеры надо заменить*

Для контакта (Contact) требуется добавить:

* поле типа «список» с названием «Тип» и значениями «Хороший», «Плохой».
* поле типа «ссылка» с названием «Соц. сеть».
* поле типа «Checkbox» с названием «Проверен».

Для Компании (Company):

* строковое поле с названием «Cчет» — расчетный счет клиента.

.. code-block:: 

    curl -X 'PATCH' \
    'https://crm.kontur.ru/api/v1/testswaggerspace/settings' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer fa1036cb0805c4b682cc81634eb6ecdd338f1e20908a2b9491e82c3da4dc8a8f' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{
    "operations": [
    {
    "op": "add",
    "path": "/customFields/contact",
    "value": {
    "id": "socialLink",
    "name": "Соц. сеть",
    "description": "Ссылка на социальную сеть",
    "type": "url"
    }
    },
    {
    "op": "add",
    "path": "/customFields/contact",
    "value": {
    "id": "typeContact",
    "name": "Тип",
    "description": "Тип",
    "type": "select",
    "options": [
    {
    "id": "good",
    "name": "Хороший"
    },
    {
    "id": "bad",
    "name": "Плохой"
    }
    ]
    }
    },
    {
    "op": "add",
    "path": "/customFields/contact",
    "value": {
    "id": "verifiedContact",
    "name": "Проверен",
    "description": "Проверенный ли контакт?",
    "type": "boolean"
    }
    },
    {
    "op": "add",
    "path": "/customFields/company",
    "value": {
    "id": "countingNum",
    "name": "Счет",
    "description": "Рассчетный счет клиента",
    "type": "text"
    }
    }
    ]
    }'

В ответ получаем 200 Ok и актуальные настройки пространства, модель Settings.

Описание модели CustomFieldSettings из Settings.CustomFields.

.. code-block::

    {
        "id": "typeContact", //идентификатор поле, поля удалять/модифицировать 
        //в настройках можно только по id
        "name": "Тип", // Наименоваение - будет выводиться в UI
        "description": "Тип", // Описание - будет выводить в UI
        "type": "select", //тип поля
        "hidden": false, // должно ли поле быть скрытым в UI
        "readOnly": false, // пользователь в UI не может его редактировать
        "permanent": false,
        "options": [ //используется для конфигурации возмодных вариантов значенийсписков.
        //только для type = select или type = multiSelect
        {
        "id": "good",
        "name": "Хороший",
        "order": 0
        },
        {
        "id": "bad",
        "name": "Плохой",
        "order": 0
        }
        ],
        "uiSettings": {} //используется для настройки отображения поля в UI, подробнее ниже и в Swagger.
  }




