.. _`POST СommunicationsСall`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcall
.. _`POST CommunicationsHangup`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2F%7Bid%7D%2Fhangup
.. _`POST TelephonyCallStarted`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-started
.. _`POST TelephonyCallEvent`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-event
.. _`POST TelephonyCallFinished`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-finished
.. _`POST TelephonyCallFailed`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-failed
.. _`POST TelephonyCallRecording`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-recording
.. _`POST TelephonyRegisterCall`: https://developer.kontur.ru/doc/crm/method?type=post&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fregister-call
.. _`GET TelephonyCallRedirect`: https://developer.kontur.ru/doc/crm/method?type=get&path=%2Fapi%2Fv1%2F%7Bws%7D%2Fcommunications%2Fcallbacks%2Ftelephony%2Fcall-redirect


API телефонии
==============

Системные вызовы
-----------------

Контур.CRM делает системные вызовы, когда пользователь нажимает кнопку «Позвонить» или «Положить трубку» в интерфейсе CRM. Для обработки таких вызовов интеграция должна принимать вызовы по HTTP через интернет — вызовы будут происходить с серверов Контур.CRM.

В системных вызовах Контур.CRM будет передавать заголовки:

* ``X-XCOM-AccessKey`` — ключ доступа для обратных вызовов в пространство. При отправке запросов не нужно повторно сообщать API-ключ интеграции.
* ``X-XCOM-Integration-Echo`` — для ответа со стороны интеграции, а не случайного сервера. Интеграция должна вернуть содержимое заголовка в таком же заголовке ответа.

**Пример**
::

    POST api/v1/my-workspace/communications/call
    Host: my-integration.ru
    X-XCOM-AccessKey: dda...d67
    X-XCOM-Integration-Echo: 7g8...d6a

**Ответ**

**200** ::

    HTTP/1.1 200 OK
    X-XCOM-Integration-Echo:7g8...d6a

.. _rst-markup-СommunicationsСall:

Системный вызов CALL
~~~~~~~~~~~~~~~~~~~~~

Метод: `POST СommunicationsСall`_

При помощи этого метода Контур.CRM делает вызов, когда пользователь нажимает кнопку «Позвонить» в интерфейсе. В интеграции должна быть включена функциональность ``CALL`` и ``HANGUP``. Подробнее в разделе: :ref:`Включение системных вызовов<rst-markup-integrationsinstances>`.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове ``CALL``, если звонок совершается по инициативе пользователя Контур.CRM.
* ``fromUserId`` — Идентификатор абонента, который переводит звонок. 
* ``toUserId`` — Идентификатор пользователя, который принимает звонок. Заполняется при внутреннем звонке;
* ``clientPhone`` — Телефон, принимающий или совершающий звонок;

**Пример**
::

    POST /api/v1/my-worksapce/communications/call
    Host: my-integration.ru
    X-XCOM-AccessKey: dda...d67
    X-XCOM-Integration-Echo: 7g8...d6a

::

    {
    "communicationId": "30a...b4e",
    "fromUserId": "3f6...5c4",
    "toUserId": "44d...52a",
    "clientPhone": "79997775533"
    }

**Ответы**

**200** ::

"OK"

**409** ::
    
    {
    "invalidDatas": [],
    "invalidConstraints": {},
    "status": "notSupported",
    "message": "Feature Call is not supported by any integration"
    }
    
.. _rst-markup-CommunicationsHangup:

Системный вызов HANGUP
~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST CommunicationsHangup`_

При помощи этого метода Контур.CRM делает вызов, когда пользователь нажимает кнопку «Положить трубку» в интерфейсе. В интеграции должна быть включена функциональность  ``CALL`` и ``HANGUP``. Подробнее в разделе: :ref:`Включение системных вызовов<rst-markup-integrationsinstances>`.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства;
* ``Id`` — Идентификатор звонка.

**Тело запроса**

* ``realtimeCallItemId`` — Идентификатор плеча звонка в момент вызова со стороны телефонии, требуется для событий реального времени.
* ``userId`` — Идентификатор пользователя.

**Пример**
::

    POST api/v1/my-workspace/communications/hangup
    Host: my-integration.ru
    X-XCOM-AccessKey: dda...d67
    X-XCOM-Integration-Echo: ue1...11o

::

    {
    "realtimeCallItemId": "7dg...us1",
    "userId": "4a4....86b"
    }

**Ответы**

**200**
::

"OK"

**409**
::

    {
    "status": "notSupported",
    "message": "string"
    }

События реального времени
--------------------------

Интеграция должна регистрировать события реального времени, это отображает интерфейс звонка. Под такими событиями подразумеваем:

* Сообщение о начале звонка
* Сообщение о событии звонка
* Сообщение о завершении звонка
* Сообщение о неудачной попытке позвонить
* Сообщение о появлении записи разговора

.. _rst-markup-TelephonyCallStarted:

Сообщение о начале звонка
~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyCallStarted`_

Метод регистрирует сообщение о начале звонка. В теле запроса нужно указать ``externalId``, этот идентификатор отправляется в сообщении о событии звонка. 

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``timestamp`` — Момент возникновения события;
* ``communicationId`` — Идентификатор коммуникации. Передается в системном вызове CALL, если звонок совершается по инициативе пользователя Контур.CRM;
* ``externalId`` — Уникальный идентификатор всего звонка;
* ``externalVatsPhone`` — Внешний номер;
* ``direction`` — Направление вызова: ``inbound`` (входящий), ``outbound`` (исходящий), ``internal`` (внутренний);
* ``clientPhone`` — Телефон, принимающий или совершающий звонок.

**Пример**
::

    POST api/v1/my-workspace/communications/callbacks/telephony/call-started
    X-XCOM-AccessKey:7fd...84a

::

    {
    "timestamp": "2022-03-22T10:38:35.6152798+00:00",
    "communicationId": "184...bcd",
    "externalId": "333...434",
    "externalVatsPhone": "79229929292",
    "clientPhone": "79997775533",
    "direction": "inbound"
    }

**Ответы**

**200**
::
    
    {
    "updateInfo": {
    "updatedAt": "2022-03-22T10:41:17.963539+00:00",
    "updatedWith": "Integration.megafon",
    "createdAt": "2022-03-22T10:38:35.176007+00:00",
    "createdWith": "Integration.megafon"
    },
    "links": {
    "companyIds": [
      "aa8a...fe6"
    ],
    "contactIds": [
      "2ee...0a6",
      "b6c...4f1"
    ],
    "dealIds": [
      "aeb7...8fe",
      "c557...d0a"
    ]
    },
    "externalId": "Megafon/333...434",
    "externalCreatedAt": "2022-03-22T10:38:35.176007+00:00",
    "type": "call",
    "direction": "inbound",
    "status": "sealed",
    "integrationId": "7a1...523",
    "data": {
    "call": {
        "clientPhone": "79997775533",
        "externalVatsPhone": "79229929292",
        "items": [
        {
          "id": "333...434",
          "from": {
            "type": "client"
          },
          "to": {
            "type": "user"
          },
          "recordings": [],
          "finishedAt": "2022-03-22T10:38:47.1835703+00:00"
        }
        ],
        "events": [
        {
        "externalCallItemId": "333...434",
        "realtimeCallItemId": "333...434",
        "timestamp": "2022-03-22T10:38:35.6152798+00:00",
        "type": "appeared",
        "from": {
        "type": "client"
            },
            "to": {
             "type": "user"
            }
        },
        {
          "externalCallItemId": "333...434",
          "realtimeCallItemId": "333...434",
          "timestamp": "2022-03-22T10:38:47.1835703+00:00",
          "type": "disconnected",
          "from": {
            "type": "client"
            },
            "to": {
            "type": "user"
        }
        }
        ]
        }
    },
    "assignedToGroupId": "000...000",
    "id": "184...bcd"
    }

**409**
::

    {
    "errors": {
    "direction": [
        "Error converting value \"in2bound\" to type 'Xcom.Api.Models.Communications.CommunicationDirection'. Path 'direction', line 7, position 27."
    ],
    "callStartedInfo": [
      "The callStartedInfo field is required."
    ]
    },
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "One or more validation errors occurred.",
    "status": 400,
    "traceId": "00-1...a-00"
    }

.. _rst-markup-TelephonyCallEvent:

Сообщение о событии звонка
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyCallEvent`_

Метод регистрирует сообщение о звонке, когда произошло одно из событий:

* Поступил вызов;
* Подняли трубку;
* Положили трубку;
* Поставили на удержание.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове ``CALL``, если звонок совершается по инициативе пользователя Контур.CRM;
* ``externalId`` — Уникальный идентификатор всего звонка;
* ``externalCallItemId`` — Идентификатор плеча звонка со стороны телефонии;
* ``realtimeCallItemId`` — Идентификатор плеча звонка в момент вызова со стороны телефонии, требуется для событий реального времени;
* ``timestamp`` — Время возникновения события;
* ``type`` — Тип события: ``appeared`` (появился), ``connected`` (подключен) ``disconnected`` (отключен), ``paused`` (пауза), ``finished`` (завершено);
* ``from`` — Участник плеча, совершающий звонок;
    #. ``type`` — Тип клиента: пользователь (``user``) или клиент (``client``);
* ``to`` — Участник плеча, принимающий звонок;
    #. ``type`` — Тип клиента: пользователь (``user``) или клиент (``client``);
    #. ``userId`` — Если тип клиента пользователь (``user``), то это определяет идентификатор пользователя.

**Пример**
::

    POST api/v1/my-workspace/communications/callbacks/telephony/call-event
    X-XCOM-AccessKey: dda...d67

::

    {
    "communicationId": "435...68e",
    "externalId": "Megafon/262...280",
    "externalCallItemId": "262...280",
    "realtimeCallItemId": "262...280",
    "timestamp": "2022-03-17T10:19:05.5106605+00:00",
    "type": "appeared",
    "from": {
        "type": "client",
    },
    "to": {
        "type": "user",
        "userId": "ae9...53d"
    }
    }

**Ответы**

**200**
::

"OK"

**409**
::

    {
    "status": "communicationNotFound",
    "message": "Communication not found. Id: 435...68e"
    }

.. _rst-markup-TelephonyCallFinished:

Сообщение о завершении звонка
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyCallFinished`_

Метод регистрирует сообщение о завершении звонка.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``timestamp`` — Время возникновения события;
* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове CALL, если звонок совершается по инициативе пользователя Контур.CRM;
* ``externalId`` — Уникальный идентификатор всего звонка;
* ``externalVatsPhone`` — Внешний номер;
* ``clientPhone`` — Телефон, принимающий или совершающий звонок;
* ``direction`` — Направление вызова: ``inbound`` (входящий), ``outbound`` (исходящий), ``internal`` (внутренний).

**Пример**
::

    {
    "timestamp": "2022-03-22T10:41:19.8948611+00:00",
    "communicationId": "f48...4ac",
    "externalId": "Megafon/335...952",
    "externalVatsPhone": "79229929292",
    "clientPhone": "79997775533",
    "direction": "inbound"
    }

**Ответы**

**200**
::

    "OK"

**409**
::


    {
    "status": "communicationNotFound",
    "message": "Communication not found. Id: f48...4ac"
    }   

.. _rst-markup-TelephonyCallFailed:

Сообщение о неудачной попытке позвонить
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyCallFailed`_

Метод регистрирует сообщение о неудачной попытке позвонить. В теле запроса нужно указать идентификатор коммуникации из системного вызова ``CALL``. 

Когда пользователь начинает звонок, CRM делает системный вызов CALL и просит интеграцию начать звонок. В ответ на вызов интеграция должна вернуть ответ 200. Если позвонить не удалось, то вернуть ошибочный код ответа, такую функциональность можно реализовать асинхронно.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства;

* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове ``CALL``, если звонок совершается по инициативе пользователя Контур.CRM.

**Пример**
::

    POST /api/v1/my-workspace/communications/callbacks/telephony/call-recording
    X-XCOM-AccessKey: dda...d67

::

    {
    "communicationId": "411...ba9",
    "externalId": "Megafon/644...384",
    "externalCallItemId": "644...384",
    "recordingFileId": "a75...f3a"
    }

**Ответы**

**200**
::

    "OK"

**409**
::

    {
    "status": "communicationNotFound",
    "message": "Communication not found. Id: 184...bcd"
    }

.. _rst-markup-TelephonyCallRecording:

Сообщение о появлении записи разговора
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyCallRecording`_

Метод отправляет сообщение о появлении записи разговора после загрузки файла в хранилище API Files. Позволяет быстрее привязать запись разговора к звонку.

Достаточно сохранять записи разговоров в процессе регистрации завершенных звонков, при чтении истории звонков из телефонии. Появление звонка в истории телефонии означает, что звонок завершен и запись готова.

**Параметры**

ws — Уникальное название рабочего пространства.

**Тело запроса**

* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове ``CALL``, если звонок совершается по инициативе пользователя Контур.CRM;
* ``externalCallItemId`` — Идентификатор плеча звонка со стороны телефонии;
* ``realtimeCallItemId`` — Идентификатор плеча звонка в момент вызова со стороны телефонии, требуется для событий реального времени;
* ``recordingFileId`` — Идентификатор записанного файла разговора.

**Пример**
::

    POST /api/v1/my-workspace/communications/callbacks/telephony/call-recording
    X-XCOM-AccessKey: dda...d67

::

    {
    "communicationId": "411...ba9",
    "externalId": "Megafon/644...384",
    "externalCallItemId": "644...384",
    "recordingFileId": "a75...f3a"
    }

**Ответы**

**200**
::

    "OK"    

**409**
::
    
    {
    "status": "communicationNotFound",
    "message": "Communication not found. Id: 184...bcd"
    }

.. _rst-markup-TelephonyRegisterCall:

Регистрация завершенных звонков
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `POST TelephonyRegisterCall`_

Метод регистрирует завершенный звонок. В интеграции должно быть реализовано чтение истории звонков из телефонии, регистрация состоявшихся или пропущенных звонков в Контур.CRM.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Тело запроса**

* ``externalVatsPhone`` — Внешний номер;
* ``clientPhone`` — Телефон, принимающий или совершающий звонок;
* ``items`` — Массив плеч звонка;

    #. ``id`` — Уникальный идентификатор плеча звонка;
    #. ``from`` — Участник плеча, совершающий звонок;
    #. ``to`` — Участник плеча, принимающий звонок.

* ``recordings`` — Массив записей разговоров плеч звонка;

    #. ``fileId`` — Идентификатор записи разговора;
    #. ``fileName`` — Название файла;
    #. ``contentType`` — Тип файла;
    #. ``contentLength`` — Размер файла в байтах.

* ``startedAt`` — Время приема звонка;
* ``finishedAt`` — Время завершения звонка;
* ``communicationId`` —  Идентификатор коммуникации. Передается в системном вызове ``CALL``, если звонок совершается по инициативе пользователя Контур.CRM;
* ``externalCreatedAt`` — Дата и время звонка;
* ``externalId`` — Уникальный идентификатор всего звонка;
* ``direction`` — Направление вызова: ``inbound`` (входящий), ``outbound`` (исходящий), ``internal`` (внутренний).


**Пример**
::

    POST /api/v1/my-workspace/communications/callbacks/telephony/register-call
    X-XCOM-AccessKey: dda...d67

::

    {
    "externalVatsPhone": "79229929292",
    "clientPhone": "79997775533",
    "items": [
        {
            "id": "143...68e",
            "from": {
                "type": "client",
            },
            "to": {
                "type": "user",
                "userId": "ae9...53d"
            },
            "recordings": [
                {
                    "fileId": "ceb...45e",
                    "fileName": "ceb4...45e",
                    "contentType": "audio/mpeg",
                    "contentLength": "9216"
                }
            ],
            "startedAt": "2022-03-18T07:27:54.6911428+00:00",
            "finishedAt": "2022-03-18T07:27:59.0622478+00:00"
        }
    ],
    "communicationId": "4358...68e",
    "externalCreatedAt": "2022-03-17T10:18:58.998205+00:00",
    "externalId": "262...280",
    "direction": "outbound"
    }

**Ответы**

**200**
::

    "OK"

**409**
::

    "Error"

.. _rst-markup-TelephonyCallRedirect:

Переадресация звонка на ответственного
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Метод: `GET TelephonyCallRedirect`_

Метод переадресовывает звонок на ответственного за сделку пользователя. Переадресовать звонок можно двумя способами:

По ``externalId`` — Если звонок зарегистрирован и Контур.CRM получил его уникальный идентификатор. Телефония программно перенаправляет входящий звонок на необходимый внутренний номер. Для получения информации о пользователе нужно отправить запрос, а в ответ будет возвращен список пользователей Контур.CRM.

По номеру телефона — До всех возможных событий. Телефония позволяет перенаправить звонок до получения ``externalId``, ответственного пользователя достаточно получить по номеру телефона.
Выбор способа переадресации зависит от возможностей телефонии.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства;
* ``externalId`` — Уникальный идентификатор всего звонка;
* ``phoneNumber`` — Номер телефона ответственного за сделку пользователя.

**Пример**
::


    GET api/v1/my-workspace/communications/callbacks/telephony/call-redirect?externalId=ab1...16t
    X-XCOM-AccessKey: dda...d67

::

    GET api/v1/my-workspace/communications/callbacks/telephony/call-redirect?phoneNumber=791229929292
    X-XCOM-AccessKey: dda...d67

**Ответы**

**200**
::

    {
    "userIds": [
    "ae9...53d"
    ]
    }

**409**
::

    {
    "status": "notFound",
    "message": "Communication Xcom.Api.Models.Communications.CallRedirectRequest not found"
    }
