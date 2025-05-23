---
order: 0.5
title: 📗Планировщик
---

### Как задать видео конкретные данные?

#### Способ 1: Использование «Планировщика»

Если необходимо задать каждому видео конкретное название, обложку, описание, теги, комментарий и другие параметры, можно использовать Планировщик.

**Планировщик** – это таблица Excel с названием **\[Scheduler\]**. В ней данные для видео задаются в ячейках колонок, где каждая колонка представляет определённый тип данных, а каждая строка соответствует конкретному видео. Планировщик может быть подключён как к одному, так и сразу к нескольким аккаунтам.

Для связывания Планировщика с аккаунтом необходимо:

1. Открыть таблицу \[Accounts\].

2. Перейти на второй лист с названием Linker.

3. В той же строке, где указаны данные аккаунта, в поле Scheduler указать путь к таблице Планировщика.

По умолчанию шаблон берёт данные из файлов в папке проекта. Чтобы включить использование линкера, в настройках шаблона смените режим работы потоков на `Выделенный`. Этот режим активирует работу линкера и свяжет Планировщик с аккаунтом. Кроме того, он необходим для связывания пользовательских файлов с данными.

#### Способ 2: Переопределение файлов с данными видео на пользовательские

[video:https://youtu.be/zN3jspWENxI:]