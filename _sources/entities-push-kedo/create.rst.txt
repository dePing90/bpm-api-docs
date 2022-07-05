.. _`Метод API для создания пользователя`: https://developer.kontur.ru/doc/bpm//method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fusers

Создание 
=======================

`Метод API для создания пользователя`_

Рассмотрим на примере создания пользователя. Запрос:

.. code-block::

    curl -X 'POST' \
   'https://somesite.ru/api/v1/testswaggerspace/users' \
   -H 'accept: application/json' \
   -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
   -H 'Content-Type: application/json-patch+json' \
   -d '{
       "login": "test@mail.ru",
       "firstName": "имя",
       "middleName": "отчество",
       "lastName": "фамилия",
       "settings": {
           "regionCode": "66",
       },
       "isAdmin": true
   }'



В ответ на успешное создание получим 200 OK и модель только что созданного пользователя:

.. code-block::

 {
  "updateInfo": {
    "updatedAt": "2022-06-28T10:46:21.762266+00:00",
    "updatedByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
    "updatedWith": "WebApp",
    "createdAt": "2022-06-28T10:46:21.762266+00:00",
    "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
    "createdWith": "WebApp"
  },
  "groupId": "00000000-0000-0000-0000-000000000000",
  "name": "фамилия имя отчество",
  "login": "test@mail.ru",
  "firstName": "имя",
  "middleName": "фамилия",
  "lastName": "отчество",
  "isAdmin": true,
  "isHidden": false,
  "isAuthorized": false,
  "status": "inactive",
  "settings": {
    "regionCode": "66",
    "notifications": {
      "channels": {
        "webAppEnabled": true,
        "webAppEnabledAt": "2022-06-28T10:46:21.762266+00:00"
      },
      "types": [
        {
          "id": "hotDeals",
          "channels": {
            "webAppEnabled": true,
            "emailEnabled": false,
            "telegramEnabled": false,
            "webAppEnabledAt": "2022-06-28T10:46:21.762266+00:00"
          },
          "schedule": {}
        },
        {
          "id": "task",
          "channels": {
            "webAppEnabled": true,
            "emailEnabled": false,
            "telegramEnabled": false,
            "webAppEnabledAt": "2022-06-28T10:46:21.762266+00:00"
          },
          "schedule": {}
        },
        {
          "id": "currentTasks",
          "channels": {
            "webAppEnabled": true,
            "emailEnabled": false,
            "telegramEnabled": false,
            "webAppEnabledAt": "2022-06-28T10:46:21.762266+00:00"
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
  "id": "375aebae-df86-4cc8-93f5-a0b4fb376efe" 
  }


    





