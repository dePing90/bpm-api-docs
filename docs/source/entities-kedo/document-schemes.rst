Документ-схема
==============

Документ-схема — описание полей и стандартного маршрута документа

Аргументы документ-схемы:

* Название
* Идентификатор
* Ссылка на маршрут
* Набор пользовательских полей
* Идентификатор сущности в пачке — чтобы при массовых операциях можно было поматчить ответ с запросом

.. code-block::

  "items": [
    {
      "name": "string",
      "externalId": "string",
      "routeId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "customFields": [
        {
          "id": "string",
          "name": "string",
          "description": "string",
          "type": "text",
          "hidden": true,
          "readOnly": true,
          "permanent": true,
          "options": [
            {
              "id": "string",
              "name": "string",
              "color": "string",
              "order": 0
            }
          ],
          "catalogId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "integrationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "uiSettings": {
            "text": {
              "multiLine": true
            },
            "number": {
              "format": "none",
              "unit": "string"
            },
            "timestamp": {
              "format": "short",
              "withoutTime": true
            },
            "url": {
              "openIn": "newTab"
            }
          },
          "version": "string"
        }
      ],
      "batchItemKey": "string"
    }
  ]
