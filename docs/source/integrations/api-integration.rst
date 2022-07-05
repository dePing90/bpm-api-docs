.. _`POST IntegrationsSetup`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fintegrations%2F%7Bid%7D%2Fsetup
.. _`PATCH IntegrationsInstances`: https://developer.kontur.ru/doc/crm/method?type=patch&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fintegrations%2Finstances%2F%7Bid%7D
.. _`PATCH IntegrationsInstances`: https://developer.kontur.ru/doc/crm/method?type=patch&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fintegrations%2Finstances%2F%7Bid%7D
.. _`GET IntegrationsInstances`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fintegrations%2Finstances%2F%7Bid%7D
.. _`GET UiSettings`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fui-settings%2F%7Bid%7D

API интеграции
===============

.. _rst-markup-IntegrationSetup:

Активация интеграции
---------------------

Метод: `POST IntegrationsSetup`_

Интеграция после установки находится в статусе ``NotConfigured``, метод активирует интеграцию. В теле запроса нужно указать необходимые аргументы со стороны интеграции.

**Параметры**

* ``Id`` — Идентификатор интеграции;
* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``object`` — Значение аргумента интеграции.

**Пример**
::

    {
    "SecretKey": null,
    "autoRedirect": false,
    "autoAnswer": false
    }

**Ответы**

**200** :: 

"OK"

**409** ::

    }
    "status": "IntegrationNotFound",
    "message": "Integration not found"
    }


.. _rst-markup-PatchIntegrationInstances:

Настройка webhook
------------------
Метод: `PATCH IntegrationsInstances`_

Метод регистрирует Webhook в модель ``IntegrationInstance``. Если интеграция некорректно отвечает на вызовы, то со временем Контур КЭДО перестанет их отправлять.

Контур КЭДО позволяет подписаться на события через Webhook.
**Параметры**

* ``Id`` — Идентификатор интеграции;
* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``op`` — Название операции;
* ``path`` — Элемент массива;
* ``value`` — Новое значение объекта;
* ``id`` — Уникальный идентификатор webhook;
* ``relativeUrl`` — Путь вызова события;
* ``triggerType`` — Тип триггера webhook;
* ``filter`` — Фильтр событий, если тип триггера EntityEvent;
* ``items`` — Список фильтров;

    #. ``eventType`` — Тип события;
    #. ``entityType`` — Тип события сущности;
    #. ``changeType`` — Тип изменения;

* ``schedule`` — Объект расписания;

    #. ``period`` — Период вызова для синхронизации;
    #. ``disabled`` — Определяет статус webhook.

**Пример**
::

    curl -X 'PATCH' \
    'https://somesite.ru/api/v1/my-integration/integrations/instances/e01...7d9' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer 1r3...ed8' \
    -H 'Content-Type: application/json-patch+json' \
    -d '{"operations":[{"op":"add","path":"/webHooks","value":
    {
    "id":"00000000-0000-0000-0000-000000000000",
    "relativeUrl":"setup/upgrade",
    "triggerType":"schedule",
    "filter":{"items":[]
    },
    "schedule":{"period":"00:05:00"},"disabled":false}}]}
    ]
    }'

Проверка статуса
-----------------

Метод: `GET IntegrationsInstances`_

Метод возвращает информацию об интеграции. В полученном ответе строка status определяет состояние интеграции. 

Существуют следующие статусы:

* ``NotConfigured`` = 0 — Не установлена;
* ``Active`` = 1 — Работает;
* ``Paused`` = 2 — Поставлена на паузу;
* ``HasErrors`` = 3 — Есть ошибки, но работает;
* ``Failed`` = 4 — Не работает.

**Параметры**

* ``Id`` — Идентификатор экземпляра интеграции. Совпадает с идентификатором интеграции IntegrationId.
* ``ws`` — Уникальное название рабочего пространства.

**Пример**
::
    
    GET /api/v1/my-workspace/integrations/instances/3ft...w21
    X-XCOM-AccessKey: dda...d67

**Ответы**

**200** ::

    {
     "updateInfo": {
       "updatedAt": "2021-03-12T15:07:34.312338+00:00",
       "updatedWith": "Integration.PracticReports",
       "createdAt": "2020-10-06T13:01:57.678594+00:00",
       "createdByUserId": "021c...5b5",
       "createdWith": "WebApp"
     },
     "baseUrl": "https://my-integration.ru",
     "features": {
       "call": false,
       "hangup": false,
       "sendSms": false
     },
     "status": "active",
     "secrets": [],
     "settings": [
       {
         "id": "recipients",
         "value": ""
       },
       {
         "id": "sendDay",
         "value": "Monday"
       },
       {
         "id": "sendHourUtc",
         "value": "0"
       },
       {
         "id": "version",
         "value": "string"
       }
     ],
     "webHooks": [
       {
         "id": "d817...837",
         "relativeUrl": "setup/upgrade",
         "triggerType": "schedule",
         "filter": {
           "items": []
         },
         "schedule": {
           "period": "00:05:00"
         },
         "disabled": false
       }
     ],
     "id": "6838...ed82"
   }

**409** ::

    {
    "status": "notFound",
    "message": "IntegrationInstance 838...ed82 not found"
    }