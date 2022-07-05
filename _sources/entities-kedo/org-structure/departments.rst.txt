Подразделение
=============


Подразделение (Department) - это любой структурный элемент компании: холдинг, организация (юр.лицо), филиал, отдел и т.д.

Аргументы подразделения:

* Идентификатор
* Краткое наименование
* Полное наименование
* Тип
* Родительское подразделение
* Руководитель
* Статус
* Кастомные поля

.. code-block::

  {
    "name": "string",
    "externalId": "string",
    "title": "string",
    "tipe": "departments",
    "status": "active",
    "parentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "headManger": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "customFields": {
      "additionalProp1": "string",
      "additionalProp2": "string",
      "additionalProp3": "string"
    },
    "batchItemKey": "string"
  }
