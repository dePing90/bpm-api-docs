.. _`Метод API для создания Company`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcompanies

Пример создания Клиента
=======================

`Метод API для создания Company`_

В Body передается модель CompanyCreationArgs. Формируем запрос:

.. code-block:: csharp

    curl -X 'POST' \
        'https://crm.kontur.ru/api/v1/testswaggerspace/companies' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
        -H 'Content-Type: application/json-patch+json' \
        -d '{
            "inn": "6663003127",
            "kpp": "667101001",
            "name": "Новая компания",
            "regionCode": "66",
            "description": "Тестовое создание через api",
            "phones": [
                {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "work",
                "value": "83433101111"
                }
            ]
        }'


В ответ на успешное создание получим 200 OK и модель Company только что созданной компании:

.. code-block:: csharp

    {
        "updateInfo": {
            "updatedAt": "2021-10-02T13:12:58.464901+00:00",
            "updatedByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
            "updatedWith": "WebApp",
            "createdAt": "2021-10-02T13:12:58.464901+00:00",
            "createdByUserId": "253f8b40-abe9-4643-81f2-6a6ffa4861be",
            "createdWith": "WebApp"
        },
        "inn": "6663003127",
        "kpp": "667101001",
        "name": "Новая компания",
        "description": "Тестовое создание через api",
        "messengerContacts": [],
        "phones": [
            {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "work",
            "value": "83433101111"
            }
        ],
        "emails": [],
        "regionCode": "66",
        "customFields": {},
        "tags": [],
        "id": "98479adb-9802-4856-8e8c-6380851f4ae7"
    }


