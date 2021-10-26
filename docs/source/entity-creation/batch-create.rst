.. _`Метод API для создания контактов`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcontacts%2Fcreate

Пример создания нескольких контактов
====================================

`Метод API для создания контактов`_

Пример эффективного создания нескольких контактов за один запрос к API:

В Body передается модель ContactCreationArgsBatchCreateRequest.

Если хотим «привязать» контакт к компании, то добавляем по пути «/links/companyIds» индентификатор соответствующей компании.

Формируем запрос:

.. code-block::

    curl -X 'POST' \
    'https://crm.kontur.ru/api/v1/testswaggerspace/contacts/create' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer 1d0eeae7c276a0c7011ae98819c1aaac3f4e0d14d66bbc5aff7edf23389e050a' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{
    "items": [
        {
        "position": "Главный бухгалтер",
        "links": {
            "companyIds": [
            "98479adb-9802-4856-8e8c-6380851f4ae7"
            ]
        },
        "name": "Майров Иван Васильевич",
        "regionCode": "66",
        "phones": [
            {
            "type": "unknown",
            "value": "86046851124"
            }
        ],
        },
        {
        "position": "Руководитель IT отдела",
        "links": {
            "companyIds": [
            "98479adb-9802-4856-8e8c-6380851f4ae7"
            ]
        },
        "name": "Мостовой Александр Викторович",
        "regionCode": "66",
        "phones": [
            {
            "type": "work",
            "value": "89452547894"
            }
        ],
        }
    ]
    }'

В ответ на успешное создание получим 200 OK и модель ContactBatchCreateResult только что созданной компании:

.. code-block:: c#

    {
    "items": {
        "7dfbc49b-87b0-42b6-aef6-b60b073b3664": {
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
        "position": "Главный бухгалтер",
        "name": "Майров Иван Васильевич",
        "messengerContacts": [],
        "phones": [
            {
            "id": "0efd09de-d8a9-4d30-95d5-2e1f573db685",
            "type": "unknown",
            "value": "86046851124"
            }
        ],
        "emails": [],
        "regionCode": "66",
        "customFields": {},
        "tags": [],
        "id": "aafa9f04-110f-4938-9636-ebfd057d5ef5"
        },
        "f3f70d19-cdbe-4eb9-b223-024094e72090": {
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
    }
    }

    
