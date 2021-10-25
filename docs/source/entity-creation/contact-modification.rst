.. _`Метод API для изменения контактов`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcontacts%2F%7Bid%7D 

Пример модицикации контакта
===========================

`Метод API для изменения контактов`_

Допустим, есть контакт и у него обновилась информация. 
Настоящая фамилия не Мостовой, а Бочкин и должность 
не «Руководитель IT отдела», а «Менеджер по продажам». Так же удалим телефон и добавим почту. Исходный Contact в API:

.. code-block:: c#

    {
        "updateInfo": {
            "updatedAt": "2021-10-02T13:32:00.973935+00:00",
            "updatedByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
            "updatedWith": "WebApp",
            "createdAt": "2021-10-02T13:32:00.973935+00:00",
            "createdByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
            "createdWith": "WebApp"
        },
    "links": {
        "companyIds": [
            "98479adb-9802-4856-8e8c-6380851f4ae7"
            ]
         },
    "position": "Руководитель IT отдела",
    "name": "Мостовой Александр Викторович",
    "messengerContacts": [],
    "phones": [
        {
        "id": "7ed85d94-7827-4481-9142-db07a04835a3",
        "type": "work",
        "value": "89452547894"
        }
     ],
    "emails": [],
    "regionCode": "66",
    "customFields": {},
    "tags": [],
    "id": "529edc65-e929-4957-b7b4-924126547323"
  }

Запрос на модификацию:

.. code-block:: c#
    
    curl -X 'PATCH' \
        'https://crm.kontur.ru/api/v1/testswaggerspace/contacts/529edc65-e929-4957-b7b4-924126547323' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer b21f4388c6e09b5e87fb1d2e9c179f0d0ee261dce0002820e3a98768b0e059bc' \
        -H 'Content-Type: application/json-patch+json' \
        -d '{
        "operations" : [
            { "op" : "Replace", "path": "/name", value: "Бочкин Александр Викторович"},
            { "op" : "Replace", "path": "/position", value: "Менеджер по продажам"},
            { "op" : "Remove", "path": "/phones/7ed85d94-7827-4481-9142-db07a04835a3" },
            { "op" : "Add", "path" : "/emails", "value" : { "type" : "work", "value" : "bochkin@test.ru" }}  
        ]
     }'

Ответ на запрос 200 OK и модель Contact:

.. code-block:: c#
    
    {
    "updateInfo": {
    "updatedAt": "2021-10-02T14:27:26.392842+00:00",
    "updatedByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
    "updatedWith": "WebApp",
    "createdAt": "2021-10-02T13:32:00.973935+00:00",
    "createdByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
    "createdWith": "WebApp"
    },
    "links": {
    "companyIds": [
    "98479adb-9802-4856-8e8c-6380851f4ae7"
    ]
    },
    "position": "Менеджер по продажам",
    "name": "Бочкин Александр Викторович",
    "messengerContacts": [],
    "phones": [],
    "emails": [
    {
    "id": "f96b8aa3-e215-46ed-89f3-64079f993da9",
    "type": "work",
    "value": "bochkin@test.ru"
    }
    ],
    "regionCode": "66",
    "customFields": {},
    "tags": [],
    "id": "529edc65-e929-4957-b7b4-924126547323"
    }