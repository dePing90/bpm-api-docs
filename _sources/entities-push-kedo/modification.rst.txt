.. _`Метод API для изменения пользователя`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcontacts%2F%7Bid%7D 

Изменение
===========================

`Метод API для изменения пользователя`_
*поставить правильную ссылку*

Допустим, есть пользователь и 
у него обновилась информация. Настоящая фамилия не Мостовой, а Бочкин и регион не 02, а 74. Исходный User в API:

.. code-block:: c#
    
    {
     "updateInfo": {
       "updatedAt": "2022-06-28T11:46:54.93681+00:00",
       "updatedByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
       "updatedWith": "WebApp",
       "createdAt": "2022-06-28T11:46:54.93681+00:00",
       "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
       "createdWith": "WebApp"
     },
     "name": "Мостовой Александр Викторович",
     "login": "test2@mail.ru",
     "firstName": "Александр",
     "middleName": "Викторович",
     "lastName": "Мостовой",
     "isAdmin": false,
     "isHidden": false,
     "isAuthorized": false,
     "status": "inactive",
     "settings": {
       "regionCode": "02"
     },
     "id": "e047339c-cd31-4c13-ba4b-455e3fcd60d4"
   }


Запрос на модификацию:

.. code-block::

    curl -X 'PATCH' \
   'https://somesite.ru/api/v1/testswaggerspace/users/e047339c-cd31-4c13-ba4b-455e3fcd60d4' \
   -H 'accept: application/json' \
   -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
   -H 'Content-Type: application/json-patch+json' \
   -d '{
   "operations" : [
       { "op" : "Replace", "path": "/lastname", value: "Бочкин"},
       { "op" : "Replace", "path": "/settings/regionCode", value: "74"}
   ]
   }'

Ответ на запрос 200 OK и модель User:

.. code-block:: c#
    
    {
     "updateInfo": {
       "updatedAt": "2022-06-28T11:46:54.93681+00:00",
       "updatedByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
       "updatedWith": "WebApp",
       "createdAt": "2022-06-28T11:46:54.93681+00:00",
       "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
       "createdWith": "WebApp"
     },
     "name": "Бочкин Александр Викторович",
     "login": "test2@mail.ru",
     "firstName": "Александр",
     "middleName": "Викторович",
     "lastName": "Бочкин",
     "isAdmin": false,
     "isHidden": false,
     "isAuthorized": false,
     "status": "inactive",
     "settings": {
       "regionCode": "74"
     },
     "id": "e047339c-cd31-4c13-ba4b-455e3fcd60d4"
   }
