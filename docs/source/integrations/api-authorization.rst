.. _`POST AuthorizePrivateIntegration`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2Fauthorization%2Fauthorize-private-integration
.. _`POST AuthorizeIntegration`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2Fauthorization%2Fauthorize-integration


API авторизации
================

Авторизация приватной интеграции
---------------------------------

Метод: `POST AuthorizePrivateIntegration`_

Метод авторизует публичную интеграцию и возвращает ``AccessKey``. В последующих запросах к API Контур.CRM нужно передавать ``AccessKey``. 

Для получения нужен ApiKey, который отображается по нажатию кнопки ``«Secrets»`` в пространстве интеграций по API. Полученный ``AccessKey`` нельзя хранить в долгосрочном хранилище, он выдается на короткий срок и действует 20 минут.

**Пример**
::

    POST api/v1/authorization/authorize-private-integration
    X-XCOM-Integration-ApiKey: 8d4...8a0

**Ответы**

**200** ::

    {
  "workspace": {
    "id": "d28...26b",
    "name": "my-workspace",
    "title": "Мое рабочее пространство",
    "updateInfo": {
      "updatedAt": "2022-03-17T05:14:14.541084+00:00",
      "updatedWith": "xcom",
      "createdAt": "2022-03-17T05:14:14.541084+00:00",
      "createdWith": "xcom"
    }
    },
    "integrationInstance": {
    "updateInfo": {
      "updatedAt": "2022-03-17T10:36:57.17227+00:00",
      "updatedByUserId": "ae9...53d",
      "updatedWith": "WebApp",
      "createdAt": "2022-03-17T10:36:57.17227+00:00",
      "createdByUserId": "ae9...53d",
      "createdWith": "WebApp"
    },
    "features": {
      "call": true,
      "hangup": true,
      "sendSms": true
    },
    "status": "active",
    "secrets": [],
    "settings": [],
    "webHooks": [],
    "id": "80d...91de"
    },
    "accessKey": "7fd...84a"
    }

**409** ::

    {
    "status": "notInstalled",
    "message": "Integration not installed"
    }

Авторизация публичной интеграции
---------------------------------
Метод: `POST AuthorizeIntegration`_

Метод авторизует публичную интеграцию и возвращает ``AccessKey``. При отправке заголовка нужно указать ``Integration-Secret`` — ключ доступа со стороны телефонии. В последующих запросах к API Контур.CRM нужно передавать ``AccessKey``. 

``Integration-Secret`` можно задать во время :ref:`активации интеграции<rst-markup-integrationsetup>` или :ref:`включения системных вызовов<rst-markup-integrationsinstances>`. Полученный ``AccessKey`` нельзя хранить в долгосрочном хранилище, он выдается на короткий срок и действует 20 минут.


**Пример**
::

    POST api/v1/authorization/authorize-integration
    X-XCOM-Integration-ApiKey: 8d4...8a0
    X-XCOM-Integration-Secret: secretKey=secretValue

**Ответы**

**200** ::

    {
    "workspace": {
    "id": "d28...26b",
    "name": "my-workspace",
    "title": "Мое рабочее пространство",
    "updateInfo": {
      "updatedAt": "2022-03-17T05:14:14.541084+00:00",
      "updatedWith": "xcom",
      "createdAt": "2022-03-17T05:14:14.541084+00:00",
      "createdWith": "xcom"
    }
    },
    "integrationInstance": {
    "updateInfo": {
      "updatedAt": "2022-03-17T10:36:57.17227+00:00",
      "updatedByUserId": "ae9...53d",
      "updatedWith": "WebApp",
      "createdAt": "2022-03-17T10:36:57.17227+00:00",
      "createdByUserId": "ae9...53d",
      "createdWith": "WebApp"
    },
    "features": {
      "call": true,
      "hangup": true,
      "sendSms": true
    },
    "status": "active",
    "secrets": [],
    "settings": [],
    "webHooks": [],
    "id": "80d...91de"
    },
    "accessKey": "7fd...84a"
    }

**401** ::

    "Unauthorized"

