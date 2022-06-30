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
    'https://crm.kontur.ru/api/v1/testswaggerspace/events?limit=2' \
    -H 'accept: application/json' \
    -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

Ответ 200 Ok и модель ObjectEventsList:

.. code-block::

    {
    "count":2,
    "items":[
        {
            "id":"bf5bbe99-1d50-4247-86b7-5ee2b1021e44",
            "offset":"00000000-20ac-176a-0000-0000060f5e86",
            "type":"change",
            "changeData":{
                "type":"create",
                "new":{
                "id":"43c22e9b-6d35-4521-8f77-10eaf9ea8677",
                "name":"Продажи",
                "order":0,
                "stages":[
                    {
                        "id":1,
                        "name":"В работе",
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    },
                    {
                        "id":2,
                        "name":"Отправлено предложение",
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    },
                    {
                        "id":3,
                        "name":"Оформление",
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    },
                    {
                        "id":-1,
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    },
                    {
                        "id":-2,
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    },
                    {
                        "id":0,
                        "order":0,
                        "settings":{
                            "constraints":[
                            
                            ]
                        }
                    }
                ]
                }
            },
            "entityIds":{
                "workflowId":"43c22e9b-6d35-4521-8f77-10eaf9ea8677"
            },
            "createInfo":{
                "createdAt":"2021-09-28T11:08:26.903198+00:00",
                "createdWith":"xcom"
            }
        },
        {
            "id":"3ef692f0-1c1a-4ad3-b364-90aac4daf501",
            "offset":"00000000-20ac-176a-0000-0000060f5e87",
            "type":"change",
            "changeData":{
                "type":"create",
                "new":{
                "id":"2261e2d7-5d2d-4190-89c2-7184fa9d341f",
                "name":"Менеджер",
                "accessRights":[
                    {
                        "id":"system.deals.create",
                        "level":1
                    },
                    {
                        "id":"system.tasks.create",
                        "level":1
                    }
                ]
                }
            },
            "entityIds":{
                "roleId":"2261e2d7-5d2d-4190-89c2-7184fa9d341f"
            },
            "createInfo":{
                "createdAt":"2021-09-28T11:08:26.903198+00:00",
                "createdWith":"xcom"
            }
        }
    ],
    "firstOffset":"00000000-20ac-176a-0000-0000060f5e86",
    "lastOffset":"00000000-20ac-176a-0000-0000060f5e87",
    "hasMore":true
    }

hasMore в ответе указывает, что существуют еще события после события по смещению lastOffset.
Для их получения нужно сформировать запрос, в котором в качестве offset передать lastOffset:

.. code-block:: 

    curl -X 'GET' \
        'https://crm.kontur.ru/api/v1/testswaggerspace/events?offset=00000000-20ac-176a-0000-0000060f5e87&limit=2' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

Ответ 200 Ok и модель ObjectEventsList:

.. code-block:: 

    {
    "count":2,
    "items":[
        {
            "id":"3c75d291-09c3-4c3b-8f9b-65cd80ef8580",
            "offset":"00000000-20ac-176a-0000-0000060f5e88",
            "type":"change",
            "changeData":{
                "type":"create",
                "new":{
                "id":"a9a2f13c-218f-4f17-8176-8c96b273eb18",
                "name":"Руководитель группы",
                "accessRights":[
                    {
                        "id":"system.deals.create",
                        "level":1
                    },
                    {
                        "id":"system.deals.edit",
                        "level":1
                    },
                    {
                        "id":"system.deals.delete",
                        "level":1
                    },
                    {
                        "id":"system.tasks.create",
                        "level":1
                    },
                    {
                        "id":"system.tasks.edit",
                        "level":1
                    },
                    {
                        "id":"system.tasks.delete",
                        "level":1
                    },
                    {
                        "id":"system.analytics.view",
                        "level":1
                    },
                    {
                        "id":"system.plans.edit",
                        "level":1
                    },
                    {
                        "id":"system.communications.canSendCorporateEmail",
                        "level":1
                    },
                    {
                        "id":"system.canImport",
                        "level":1
                    },
                    {
                        "id":"system.canExport",
                        "level":1
                    },
                    {
                        "id":"system.settings.edit",
                        "level":1
                    },
                    {
                        "id":"system.communications.view",
                        "level":1
                    }
                ]
                }
            },
            "entityIds":{
                "roleId":"a9a2f13c-218f-4f17-8176-8c96b273eb18"
            },
            "createInfo":{
                "createdAt":"2021-09-28T11:08:26.903198+00:00",
                "createdWith":"xcom"
            }
        },
        {
            "id":"075b12d5-fba2-4248-b407-f3bcdac576d8",
            "offset":"00000000-20ac-176a-0000-0000060f5e89",
            "type":"change",
            "changeData":{
                "type":"create",
                "new":{
                "id":"d490af0f-d7d2-40e1-8654-955b863cacd7",
                "name":"Руководитель организации",
                "accessRights":[
                    {
                        "id":"system.deals.create",
                        "level":2
                    },
                    {
                        "id":"system.deals.edit",
                        "level":2
                    },
                    {
                        "id":"system.deals.delete",
                        "level":2
                    },
                    {
                        "id":"system.tasks.create",
                        "level":2
                    },
                    {
                        "id":"system.tasks.edit",
                        "level":2
                    },
                    {
                        "id":"system.tasks.delete",
                        "level":2
                    },
                    {
                        "id":"system.analytics.view",
                        "level":2
                    },
                    {
                        "id":"system.plans.edit",
                        "level":2
                    },
                    {
                        "id":"system.communications.canSendCorporateEmail",
                        "level":2
                    },
                    {
                        "id":"system.canImport",
                        "level":2
                    },
                    {
                        "id":"system.canExport",
                        "level":2
                    },
                    {
                        "id":"system.settings.edit",
                        "level":2
                    },
                    {
                        "id":"system.communications.view",
                        "level":2
                    }
                ]
                }
            },
            "entityIds":{
                "roleId":"d490af0f-d7d2-40e1-8654-955b863cacd7"
            },
            "createInfo":{
                "createdAt":"2021-09-28T11:08:26.903198+00:00",
                "createdWith":"xcom"
            }
        }
    ],
    "firstOffset":"00000000-20ac-176a-0000-0000060f5e88",
    "lastOffset":"00000000-20ac-176a-0000-0000060f5e89",
    "hasMore":true
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
    "dealId" : "",
    "companyId" : "",
    "workflowId" : "",
    "taskId" : "", 
    "notificationId" : "", 
    "contactId" : "",
    "userId" : "",
    "groupId" : "",
    "integrationId" : "", 
    "roleId" : "",
    "communicationId" : "",
    "analyticsSettingId" : "",
    "templateId" : "",
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

Допустим, нужно синхронизировать из Контур КЭДО изменения по объектам Company.


#. Если syncedOffset не проинициализирован, то syncedOffset:= '00000000-0000-0000-0000-000000000000'.
#. Формируем запрос за событиям на получение сущностей с offset = syncedOffset и limit равным 50.
#. Фильтруем полученные события. Eсли entityIds/companyId != null, то это событие описывает либо изменение какого-то объекта Company, либо связей этого объекта.
#. На основании отфильтрованные событий. По eventType и changeDatas обновляем соответствующие сущности во внешней системе.
#. Сохраняем в syncedOffset = lastOffset из ответа.
#. Если в ответе hasMore = false, то засыпаем на какое-то время (например, 1 минута).
#. Переходим на шаг 1.


При получении изменения через ленту событий гарантируется. что будут получены все изменения.

