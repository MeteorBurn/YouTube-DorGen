---
order: 4
title: ⛔Ошибки
---

#### Уникализация видео

Если на этапе уникализации видео появляется ошибка c текстом `Device creation failed`, то в таком случае создайте текстовый файл в папке **“..\\\\YouTube-Uploader\\\\\[Config\]\\\\libs\\\\”** с названием **“ffconfig”** и в нём укажите параметр: `hwaccelauto=off`

Это отключит аппаратное ускорение при уникализации видео, использование которого может вызывать ошибку на некоторых системах или серверах.

![](./errors-2.png){width=1210px height=222px}

:::danger:true Скриншот ошибки

![](./errors.png){width=1843px height=779px}



:::