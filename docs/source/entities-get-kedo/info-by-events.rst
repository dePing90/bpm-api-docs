.. _`Метод API для получения ленты событий`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fevents

Чтение ленты событий
====================

`Метод API для получения ленты событий`_

Необходимо передать обязательный параметр ws — имя Workspace или id Workspace. 
Также есть два необязательных параметра offset — 
смещение после, которого нужно вернуть события и limit — максимальное кол-во событий в ответе.

Получение событий
-----------------

Например:

.. code-block::

    curl -X 'GET' \
    'https://xcom.kontur.ru/api/v1/testswaggerspace/events?limit=2' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

Ответ 200 Ok и модель ObjectEventsList:

.. code-block::

{
  "count": 2,
  "items": [
    {
      "id": "ce8e3443-66f4-40cb-bb7b-a683cb3ec944",
      "offset": "00000000-3699-1b36-0000-000008ac36c1",
      "type": "change",
      "changeData": {
        "type": "create",
        "new": {
          "id": "72e3809c-1ad7-4761-bc3e-50cff06d1f83",
          "name": "отчество имя фамилия",
          "login": "test3@mail.ru",
          "status": "inactive",
          "groupId": "00000000-0000-0000-0000-000000000000",
          "isAdmin": false,
          "isHidden": false,
          "lastName": "отчество",
          "settings": {
            "regionCode": "02"            
          },
          "firstName": "имя",
          "middleName": "фамилия",
          "accessRights": [],
          "customFields": {},
          "isAuthorized": false
        }
      },
      "entityIds": {
        "userId": "72e3809c-1ad7-4761-bc3e-50cff06d1f83"
      },
      "createInfo": {
        "createdAt": "2022-06-28T11:46:54.93681+00:00",
        "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
        "createdWith": "WebApp"
      }
    },
    {
      "id": "e63e221b-fe36-438a-9def-b9909fd8938d",
      "offset": "00000000-3699-2055-0000-000008ac36c9",
      "type": "change",
      "changeData": {
        "type": "patch",
        "old": {
          "id": "e047339c-cd31-4c13-ba4b-455e3fcd60d4",
          "name": "отчество имя фамилия",
          "login": "test2@mail.ru",
          "status": "inactive",
          "groupId": "00000000-0000-0000-0000-000000000000",
          "isAdmin": false,
          "isHidden": false,
          "lastName": "отчество",
          "settings": {
            "regionCode": "02"
          },
          "firstName": "имя",
          "middleName": "фамилия",
          "accessRights": [],
          "customFields": {},
          "isAuthorized": false
        },
        "new": {
          "id": "e047339c-cd31-4c13-ba4b-455e3fcd60d4",
          "name": "Бочкин имя фамилия",
          "login": "test2@mail.ru",
          "status": "inactive",
          "groupId": "00000000-0000-0000-0000-000000000000",
          "isAdmin": false,
          "isHidden": false,
          "lastName": "Бочкин",
          "settings": {
            "regionCode": "74"
          },
          "firstName": "имя",
          "middleName": "фамилия",
          "accessRights": [],
          "customFields": {},
          "isAuthorized": false
        }
      },
      "entityIds": {
        "userId": "e047339c-cd31-4c13-ba4b-455e3fcd60d4"
      },
      "createInfo": {
        "createdAt": "2022-06-28T12:02:58.317662+00:00",
        "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
        "createdWith": "WebApp"
      }
    }
  ],
  "firstOffset": "00000000-3699-1b36-0000-000008ac36c1",
  "lastOffset": "00000000-3699-2055-0000-000008ac36c9",
  "hasMore": true
}

hasMore в ответе указывает, что существуют еще события после события по смещению lastOffset.
Для их получения нужно сформировать запрос, в котором в качестве offset передать lastOffset:

.. code-block:: 

    curl -X 'GET' \
        'https://xcom.kontur.ru/api/v1/testswaggerspace/events?offset=00000000-3699-2055-0000-000008ac36c9&limit=2' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

Ответ 200 Ok и модель ObjectEventsList:

.. code-block:: 

{
  "count": 1,
  "items": [
    {
      "id": "1bbbdaad-b5d5-42a2-b492-45dd9629b840",
      "offset": "00000000-36a1-7ea5-0000-000008ac9865",
      "type": "change",
      "changeData": {
        "type": "create",
        "new": {
          "id": "27f9a6ef-a248-4afc-bd7b-e61725ba8ca3",
          "date": "2022-06-30T21:59:59.999+03:00",
          "text": "Задача",
          "typeId": "00000000-0000-0000-0000-000000000000",
          "contactIds": [],
          "isCompleted": false,
          "supervisors": [],
          "assignedToUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
          "assignedToGroupId": "00000000-0000-0000-0000-000000000000",
          "attachmentFileIds": [],
          "sendToExternalChannels": true
        }
      },
      "entityIds": {
        "taskId": "27f9a6ef-a248-4afc-bd7b-e61725ba8ca3"
      },
      "createInfo": {
        "createdAt": "2022-06-30T10:37:23.203317+00:00",
        "createdByUserId": "0ab0dc94-616c-4b86-a074-250e76b5e63c",
        "createdWith": "WebApp"
      }
    }
  ],
  "firstOffset": "00000000-36a1-7ea5-0000-000008ac9865",
  "lastOffset": "00000000-36a1-7ea5-0000-000008ac9865",
  "hasMore": false
}

Когда в ответе будет получен hasMore = false — все события на текущий момент были прочитаны.

Описание модели ответа
----------------------

Модель ObjectEventsList имеет следующую структуру:

.. code-block:: 

    {
        "count" : 2, //кол-во событий в ответе
        "items" : [...], //массив событий каждое событие описывается моделью ObjectEvent
        "firstOffset" : "00000000-20ac-176a-0000-0000060f5e88", //смешение первого события в ответе
        "lastOffset": "00000000-20ac-176a-0000-0000060f5e89", //смешение последнего события в ответе
        "hasMore": true //есть ли события после последнего события из ответа
    }

Модель ObjectEvent:

.. code-block:: 

    {
    "id": "3c75d291-09c3-4c3b-8f9b-65cd80ef8580", // идентификатор события
    "offset": "00000000-20ac-176a-0000-0000060f5e88", // смещение события
    "type": "change", // тип change - изменение сущности, link/unlink - изменения связей с сущностью
    "createInfo" : { //иформация о времени создания события
    "createdAt" : "2021-09-28T11:08:26.903198+00:00", // время создания когдасобытия
    "createdByUserId": "7489f14b-f11b-4e13-83c4-276a183caf82", //идентификатор полльзователя создавшего событие
    "createdWith" : "WebApp", // имя приложения с использованием, которого было создано событие
    },
    "entityIds" : { // идентификаторы сущностей к которым отсится событе, если type = change, то будет представлено ровно одно поле
    // из списка ниже. Если событие об изменении связей между объектами link/unlink, то будут представлены
    // идентификаторы объектов м/у которыми изменилась связь, например companyId-dealId.
    // идентификаторы сущностей представлены в виде строк-GUID, в ответе будут представлены только id по которым
    // были изменения 
    "taskId" : "", 
    "notificationId" : "", 
    "userId" : "",
    "groupId" : "",
    "integrationId" : "", 
    "roleId" : "",
    "communicationId" : "",
    "documentId" : "",
    "routeId" : "",
    "catalogItemId" : ""
    },
    "changeData" : { //описание изменения сущности, которое произошло
    "type" : "patch", //тип изменения create, patch, delete, restore
    "old" : {}, // описание объекта перед изменением. Для изменений create/restore тут будет null,
    // для patch/delete - json сериализованное представление объекта.
    // Например, для если событие описывает PATCH Company здесь будет json модели Company
    "new" : {}, // описвание объекта после изменения. Для delete здесь будет null.
    }
    }

Алгоритм синхронизации
----------------------

Допустим, нужно синхронизировать из Контур КЭДО изменения по объектам User.


#. Если syncedOffset не проинициализирован, то syncedOffset:= '00000000-0000-0000-0000-000000000000'.
#. Формируем запрос за событиям на получение сущностей с offset = syncedOffset и limit равным 50.
#. Фильтруем полученные события. Eсли entityIds/userId != null, то это событие описывает либо изменение какого-то объекта User, либо связей этого объекта.
#. На основании отфильтрованные событий. По eventType и changeDatas обновляем соответствующие сущности во внешней системе.
#. Сохраняем в syncedOffset = lastOffset из ответа.
#. Если в ответе hasMore = false, то засыпаем на какое-то время (например, 1 минута).
#. Переходим на шаг 1.


При получении изменения через ленту событий гарантируется, что будут получены все изменения.

