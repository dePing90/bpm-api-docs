.. _`Метод API для создания нескольких пользователей`: https://developer.kontur.ru/doc/bpm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fusers%2Fcreate

Создание пачки
====================================

`Метод API для создания нескольких пользователей`_

Рассмотрим пример эффективного создания нескольких пользователей за один запрос к API. 
В Body передается модель UserCreationArgsBatchCreateRequest.
Формируем запрос:

.. code-block::

    curl -X 'POST' \
    'https://xcom.kontur.ru/api/v1/testswaggerspace/users/create' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{
    "items": [
        {
            "login": "test2@mail.ru",
            "firstName": "имя",
            "middleName": "отчество",
            "lastName": "фамилия",
        },
        {
            "login": "test3@mail.ru",
            "firstName": "имя",
            "middleName": "отчество",
            "lastName": "фамилия",
        }
    ]
    }'


В ответ на успешное создание получим 200 OK:

.. code-block:: c#

    {
    "items": {
        "a8214dc2-454d-4943-8132-25e5085a986e": {
        "updateInfo": {
            "updatedAt": "2022-06-28T11:46:54.93681+00:00",
            "updatedByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
            "updatedWith": "WebApp",
            "createdAt": "2022-06-28T11:46:54.93681+00:00",
            "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
            "createdWith": "WebApp"
        },
        "groupId": "00000000-0000-0000-0000-000000000000",
        "name": "фамилия имя отчество",
        "login": "test2@mail.ru",
        "firstName": "имя",
        "middleName": "отчество",
        "lastName": "фамилия",
        "isAdmin": false,
        "isHidden": false,
        "isAuthorized": false,
        "status": "inactive",
        "settings": {
            "regionCode": "02",
            "notifications": {
            "channels": {
                "webAppEnabled": true,
                "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
            },
            "types": [
                {
                "id": "hotDeals",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {}
                },
                {
                "id": "task",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {}
                },
                {
                "id": "currentTasks",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {
                    "time": "09:00:00",
                    "skipHolidays": true
                }
                }
            ]
            }
        },
        "customFields": {},
        "accessRights": [],
        "id": "e047339c-cd31-4c13-ba4b-455e3fcd60d4"
        },
        "80794311-a775-4a14-a9ce-f26ef8ce5123": {
        "updateInfo": {
            "updatedAt": "2022-06-28T11:46:54.93681+00:00",
            "updatedByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
            "updatedWith": "WebApp",
            "createdAt": "2022-06-28T11:46:54.93681+00:00",
            "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
            "createdWith": "WebApp"
        },
        "groupId": "00000000-0000-0000-0000-000000000000",
        "name": "фамилия имя отчество",
        "login": "test3@mail.ru",
        "firstName": "имя",
        "middleName": "отчество",
        "lastName": "фамилия",
        "isAdmin": false,
        "isHidden": false,
        "isAuthorized": false,
        "status": "inactive",
        "settings": {
            "regionCode": "02",
            "notifications": {
            "channels": {
                "webAppEnabled": true,
                "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
            },
            "types": [
                {
                "id": "hotDeals",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {}
                },
                {
                "id": "task",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {}
                },
                {
                "id": "currentTasks",
                "channels": {
                    "webAppEnabled": true,
                    "emailEnabled": false,
                    "telegramEnabled": false,
                    "webAppEnabledAt": "2022-06-28T11:46:54.93681+00:00"
                },
                "schedule": {
                    "time": "09:00:00",
                    "skipHolidays": true
                }
                }
            ]
            }
        },
        "customFields": {},
        "accessRights": [],
        "id": "72e3809c-1ad7-4761-bc3e-50cff06d1f83"
        }
    }
    }
