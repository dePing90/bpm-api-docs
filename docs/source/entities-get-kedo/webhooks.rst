Подписка на события об изменениях — WebHook
===========================================

Crm.Kontur предоставляет возможность интеграции подписаться на уведомления о событиях через механику WebHook's.

#. При настройке WebHook указываются фильтры на события, по которым нужно получать оповещения. Если в фильтре указан только User, то события об изменении Document не должно приходить.
#. При оповещении в ответ Crm.Kontur ожидает получить 200 OK и заголовок X-XCOM-Integration-Echo из входящего запроса. Если подтверждение не будет получено, система отложит событие "в очередь отложенной отправки" и попытается отправить следующее событие.
#. Модель события ObjectEvent — описана в Варианте 2. Чтением ленты событий. (предыдущий раздел).

Событие из очереди отложенной отправки Crm.Kontur будет пытаться отправить 
повторно со следующими интервалами: 30сек, 1мин, 5мин, 15мин, 1ч, 1ч, 1ч.

Если интеграция не корректно отвечает на достаточно большее кол-во запросов Контур CRM 
перестанет отправлять ей оповещения о событиях.

Для того, чтобы зарегистрировать WebHook для интеграции необходимо отправить запрос.

Для регистрации WebHook нужно добавить его в модель IntegrationInstance:

.. code-block:: 

    curl -X 'PATCH' \
        'https://xcom.kontur.ru/api/v1/testswaggerspace/integrations/instances/e01c765d-7c9b-491a-b5ea-d0e67eb017d9' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
        -H 'Content-Type: application/json-patch+json' \
        -d '{
        "operations" : [
        { "op" : "Add", "path" : "/IntegrationInstance", "value" : {"id":"a5aad3c1-777b-4ae5-8ca1-60b94c0423e5","relativeUrl":"https://publicUrl.ru/callbacks","triggerType":"entityEvent","filter":{"items":[{"eventType":"change","entityType":"company","changeType":"patch"},{"entityType":"contact"}]},"schedule":{},"disabled":false}
        }
    ]
    }'

В IntegrationInstance есть массив зарегистрированных WebHook. Описание модели WebHook:

.. code-block:: 

    {
        "id":"a5aad3c1-777b-4ae5-8ca1-60b94c0423e5", // идентификатор 
        "relativeUrl":"/callbacks", // url, куда будут отправляться оповещения о событиях
        "triggerType":"entityEvent", // triggerType бывает: 
                                    // entityEvent - заполняется блок filter - для фильтрации событий
                                    // schedule - заполняется блок Schedule - где можно настроить периодические вызовы 'relativeUrl'
        "filter":{ // блок настройки фильтров для событий
        "items":[
            {
            "eventType" : "change", // тип события: сhange / link / unlink
            "entityType" : "user", // сущность, по которой хочется получать уведомдения
            "changeType" : "patch" // тип модификации: create / patch / delete / restore
            },
            { // оповещать о всех событиях по contact
            "entityType":"user"
            }
            ]
            },
        "schedule":{
        
        },
        "disabled":false // активен ли WebHook для отправки
    }