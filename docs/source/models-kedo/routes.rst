Маршруты согласований
=====================

Маршрут согласования — это путь, который проходит документ. В маршруте может быть разное количество этапов, 
на каждом их которых пользователи согласуют, подписывают или ознакамливаются с документом.

Аргументы маршрута:

* Название
* Идентификатор
* Набор узлов маршрута

.. code-block::

    object
    {
    name: string
    externalId: string
    nodes: array of objects [
        object {
        id:
        string
        <uuid>
        name:
        string
        taskType:
        string
        nextNodeIds:
    array of strings
    [
    string
    <uuid>
    startNodeId:
    string
    <uuid>
    batchItemKey: