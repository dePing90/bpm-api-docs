Документ
=========

Документ — экземпляр, который создан на основе конкретной Документ-схемы.

Аргументы документа:

* Название
* Идентификатор
* Идентификатор документ-схемы
* Дата создания
* Набор пользовательских полей
* Идентификатор сущности в пачке — чтобы при массовых операциях можно было поматчить ответ с запросом

.. code-block::

  {
    "name": "string",
    "externalId": "string",
    "documentSchemeId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "initiatorUserId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "externalCreatedAt": "2022-06-29T14:05:08.050Z",
    "customFields": {
      "additionalProp1": "string",
      "additionalProp2": "string",
      "additionalProp3": "string"
    },
    "batchItemKey": "string"
  }
