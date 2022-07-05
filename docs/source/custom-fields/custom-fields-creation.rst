Создание через API
===============================


Контур КЭДО позволяет добавлять пользовательские поля в основные сущности системы: 

* Пользователя (User) 
* Документы (Documents)

Для того, чтобы добавить пользовательское поле в сущность, необходимо объявить 
его в настройках (Settings) рабочего пространства (Workspace).

Метод API:

.. code-block:: 

    PATCH https://somesite.ru/api/v1/{ws}/settings


В модели Settings есть поле CustomFields, в котом описываются пользовательские поля.

Для пользователя (User) требуется добавить:

* поле типа «список» с названием «Тип» и значениями «Хороший», «Плохой».
* поле типа «ссылка» с названием «Соц. сеть».
* поле типа «Checkbox» с названием «Проверен».

.. code-block:: 

    curl -X 'PATCH' \
    'https://somesite.ru/api/v1/testswaggerspace/settings' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{
  "operations": [
    {
      "op": "add",
      "path": "/customFields/user",
      "value": {
        "id": "socialLink",
        "name": "Соц. сеть",
        "description": "Ссылка на социальную сеть",
        "type": "url"
      }
    },
    {
      "op": "add",
      "path": "/customFields/user",
      "value": {
        "id": "type",
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
      "path": "/customFields/user",
      "value": {
        "id": "verifiedUser",
        "name": "Проверен",
        "description": "Проверен?",
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
        "id": "type", //идентификатор поле, поля удалять/модифицировать 
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



Для добавления или изменения полей в документе необходимо 
внести правки в соответствующей схеме документа.

.. code-block::

    curl -X 'PATCH' \
    'https://somesite.ru/api/v1/testswaggerspace/document-schemes/{scheme-id}' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{
  "operations": [
    {
      "op": "add",
      "path": "/customFields",
      "value": {
        "id": "socialLink",
        "name": "Соц. сеть",
        "description": "Ссылка на социальную сеть",
        "type": "url"  
        }
    }
  ]
  }'
   
   

