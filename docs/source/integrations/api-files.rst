.. _rst-markup-UploadFile:

API files
==========

Загрузка файла
---------------

Метод загружает файл на сервер Контур КЭДО.

В ответ возвращается метаинформация о загруженном файле. Максимальный размер загружаемого файла — 100 мегабайт. Загруженный файл в Контур КЭДО попадает во временное хранилище и находится там 1 день, ему присваивается временный идентификатор.

Сохранять идентификатор загруженного файла на долгий срок не нужно. Привязка файла к сущности происходит при помощи методов создания/сохранения сущности (например, идентификатор файла может быть записан в пользововательское поле типа "файл"). После чего файл переносится в постоянное хранилище с постоянным идентификатором.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства.

**Пример**
::

    POST api/v1/my-workspace/files
    X-XCOM-AccessKey: dda...d67
    Content-Type: multipart/form-data; boundary="boundary"

::

    --boundary
    Content-Disposition: form-data; name="file"; filename="example.txt"
    Content-Type: text/plain
  
    Hello, world!
    --boundary--

**Ответы**

**200** ::

    {
    fileId: "a75...f3a",
    fileName: "example.txt",
    contentType: "text/plain",
    contentLength: 13
    }

**409** ::

    {
    "status": "fileTooLarge",
    "message": "File Too Large. Id: 3fa...fa6"
    }

.. _rst-markup-FileById:

Скачивание файла
-----------------

Метод скачивает файл с сервера Контур КЭДО.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства;
* ``fileId`` — Идентификатор файла.

**Пример**
::

    GET api/v1/my-workspace/files/a75...f3a
    X-XCOM-AccessKey: dda...d67

**200** ::

    HTTP/1.1 200 OK
    "Content-Type": "application/json; charset=utf-8",
    "Content-Length": "162"
    Hello, world!

Дополнительно можно передать параметр ``download=true`` для запуска скачивания файла. Это полезно, если скачивание файла происходит через браузер, в ответ выставляется заголовок ``Content-Disposition``. С этим заголовком браузер не будет пытаться открыть файл, если даже умеет это делать. 

**Пример**
::

    GET api/v1/my-workspace/files/a75...f3a?download=true
    X-XCOM-AccessKey: dda...d67

**Ответ**

**200 download=true**
::

    HTTP/1.1 200 OK
    "Content-Type": "application/json; charset=utf-8",
    "Content-Length": "162"
    Content-Disposition: attachment; filename="admin_out_2022_03_22-13_37_05_79997775533_da7d.mp3"
  
    Hello, world!

.. _rst-markup-MetaById:

Получение метаинформации
-------------------------

Метод возвращает метаинформацию о файле.

**Параметры**

* ``ws`` — Уникальное название рабочего пространства;
* ``fileId`` — Идентификатор файла.

**Пример**
::

    GET api/v1/my-workspace/files/3fa...fa6/meta
    X-XCOM-AccessKey: dda...d67

**Ответ**

**200** ::

    {
    "fileId": "a75...f3a",
    "fileName": "admin_out_2022_03_22-13_37_05_79997775533_da7d.mp3",
    "contentType": "audio/mpeg",
    "contentLength": "11735"
    }

Метод: `HEAD Files`_

Метод возвращает заголовки о метаинформации файла.

**Пример**
::

    HEAD api/v1/my-workspace/files/a75...f3a
    X-XCOM-AccessKey: dda...d67

**Ответ**

**200 HEAD** ::

    HTTP/1.1 200 OK
    "Content-Type": "application/json; charset=utf-8",
    "Content-Length": "162"

