---
order: 1
title: 📘 Руководство
---

Руководство для тех, кто хочет заказать парсинг YouTube как услугу или самостоятельно извлечь данные с помощью шаблона **YouTube-Parser.**

Данный материал будет полезен как владельцам YouTube-Parser, так и тем, кто впервые столкнулся с задачей парсинга данных с YouTube. В руководстве подробно рассматриваются особенности сбора данных, действующие ограничения и способы получения максимального количества релевантных результатов в заданной тематике.

### 1\. Входные данные для парсинга YouTube

Поиск информации на YouTube работает по тому же принципу, что и в других поисковых системах, таких как Google, Yandex или Yahoo. Для получения нужных данных необходимо указать входной параметр -- **поисковой запрос** (ключевая фраза или ключ). Поисковой запрос вводится в строку поиска, после чего YouTube возвращает результаты, соответствующие тематике запроса.

Функции наподобие: **«спарсить всё»**, **«собрать каналы  из СНГ с аудиторией от 10 000 подписчиков»** или **«найти криптовалютные каналы из США»** отсутствуют и не предусмотрены. YouTube не предоставляет возможности фильтрации данных по аудитории, категории контента, странам, количеству подписчиков, просмотрам или частоте публикации видео. Единственный доступный способ поиска каналов, видео и плейлистов -- **введение поискового запроса в строку поиска YouTube** и анализ полученных результатов.

Например, для поиска каналов на криптовалютную тематику можно использовать следующие поисковые запросы:

-  `Trending DeFi tokens`

-  `Crypto Exchange`

-  `Crypto passive income`

В ответ YouTube выдаст релевантные результаты, соответствующие введённым запросам.

### 2\. Ограничение поисковой выдачи YouTube

YouTube накладывает ограничение на количество результатов, возвращаемых по одному поисковому запросу -- не более `600` результатов. Это означает, что при вводе одного запроса невозможно получить более `600` каналов, видео или плейлистов. **Обойти это ограничение невозможно!**

Фактическое количество доступных результатов зависит от популярности поискового запроса. Если запрос востребован, YouTube предоставит максимальное возможное количество записей, но не более `600`. Чтобы получить больше данных в нужной тематике, рекомендуется использовать **разные поисковые запросы**. Чем больше различных запросов указано в качестве входных данных для парсинга, тем больше можно собрать уникальных каналов, видео и плейлистов.

### 3\. Этапы парсинга YouTube

Парсинг данных с YouTube чаще всего выполняется в несколько этапов:

1. **Парсинг поисковой выдачи** по видео, каналам или плейлистам.

2. **Парсинг расширенной информации** о каналах, видео и плейлистах на основе собранных ссылок из поисковой выдачи.

YouTube предоставляет в результатах поиска лишь ограниченный набор данных о найденных сущностях. Например, такие данные, как: количество подписчиков, просмотров, лайков, полное описание видео, дату публикации, страну канала и другие нельзя получить напрямую из поисковой выдачи. Для сбора этих данных необходимо делать **отдельные запросы** к YouTube по каждой найденной сущности.

Допустим, требуется найти детские каналы с **количеством подписчиков от 5000 и созданные до 2022 года.** В таком случае процесс парсинга будет состоять из 2 этапов:

1. Сначала собираются ссылки на каналы по тематическим поисковым запросам.

2. Затем по каждой найденной ссылке выполняется дополнительный парсинг информации о канале (количество подписчиков, дата создания и т. д.).

В некоторых случаях может понадобиться третий этап парсинга. Например, если требуется:

-  собрать ссылки на социальные сети

-  получить полный список опубликованных видео на канале,

-  отобрать каналы по дате публикации видео, количеству просмотров, лайков и другим параметрам.

Если парсинг выполняется на заказ, то **каждый этап оплачивается отдельно** в соответствии с актуальными ценами.

### 4\. Почему лучше парсить выдачу по видео?

При поиске тематических каналов в поисковой выдаче рекомендуется парсить видео, а не каналы.

**Почему не стоит парсить выдачу по каналам?**\
Если использовать поиск по каналам, YouTube возвращает только те каналы, в названии которых содержатся все или часть слов из поискового запроса в точном порядке. Это означает, что:

-  Название канала обязательно должно включать искомую фразу или её часть.

-  Количество найденных каналов будет значительно ограничено, так как многие тематические каналы могут не содержать ключевые слова запроса в названии.

**Почему лучше парсить выдачу по видео?**\
Если искать по видео, YouTube возвращает результаты двух типов:

1. Видео с точным совпадением поисковой фразы в названии.

2. Видео, которые относятся к тематике запроса, даже если заголовок не содержит все ключевые слова.

Это возможно благодаря алгоритмам YouTube, которые анализируют содержание видео и относят его к определённой тематике, даже если в названии нет точного совпадения с поисковым запросом.

Таким образом, парсинг поисковой выдачи по видео позволяет обнаружить больше релевантных каналов, которые публикуют контент в нужной тематике.

💡 **Оптимальный вариант** – комбинировать оба метода:

-  Использовать поиск по видео для сбора максимально широкой базы тематических каналов.

-  Дополнительно применять поиск по каналам, если необходимо найти каналы с определёнными ключевыми словами в названии.

### 5\. Фильтрация результатов

Фильтрация данных позволяет исключить нежелательные сущности из результатов парсинга. Она может выполняться двумя способами:

1. **Фильтрация во время парсинга** – выполняется средствами **YouTube-Parser**.

2. **Фильтрация после парсинга** – осуществляется в **таблице отчёта** с использованием фильтров и условий в **Microsoft Excel**.

Рекомендуется применять фильтрацию в Microsoft Excel, так как это даёт больше возможностей:

✅ Использование сложных критериев и условий фильтрации.

✅ Возможность отменить исключённые результаты и применить новые значения фильтров без повторного сбора данных.

**Как влияет фильтрация во время парсинга?**

Если включить фильтрацию на этапе парсинга в YouTube-Parser, это не замедляет процесс сбора данных – скорость остаётся неизменной.

### 6\. Методы парсинга

В **YouTube-Parser** реализованы два метода парсинга, которые можно выбирать в зависимости от типа собираемых данных или поставленной задачи:

1. **YouTube Data API v3** – официальный API, предназначенный для удобного получения данных из YouTube.

2. **InnerTube API** – приватное API, используемое самим YouTube для взаимодействия по модели «клиент-сервер», например, при загрузке контента в браузере.

#### YouTube Data API v3

Метод YouTube Data API v3 считается основным в YouTube-Parser, так как он:

-  Обеспечивает стабильную работу.

-  Гарантирует максимальную скорость получения данных.

-  Позволяет извлекать подавляющее большинство доступной информации.

#### InnerTube API

Некоторые данные доступны только через InnerTube API, поскольку:

-  YouTube Data API v3 не предоставляет все возможные методы получения информации.

-  YouTube ограничивает доступ к определённым данным через официальный API.

**Примеры функций, которые работают исключительно через InnerTube API:**

-  Парсинг трендов

-  Парсинг постов канала

-  Парсинг комментариев к постам

-  Парсинг ссылок на социальные сети канала

-  Скачивание видео

-  Скачивание субтитров

#### Выбор метода парсинга

Некоторые функции поддерживают оба метода, и пользователь может выбрать подходящий вариант.\
Используемый метод влияет на доступные поля данных в таблице с результатами. Метод парсинга можно изменить на первой вкладке `Входных настроек`**.**

### 7\. YouTube API Keys

Для парсинга данных с использованием **YouTube Data API v3** необходимы **специальные API-ключи** (**API Keys**) -- это уникальная строка длиной **39 символов**, через которую осуществляется доступ к API YouTube и получение данных.

#### **Как работает квота API-ключей?**

-  У каждого ключа есть суточная квота -- 10 000 поинтов, которые расходуются при каждом обращении к API.

-  За каждую операцию списывается фиксированное количество поинтов.

-  Квота обновляется каждые сутки, что позволяет использовать ключ неограниченное количество раз, но в рамках лимита.

-  Чем больше ключей – тем больше данных можно собрать в течение суток.

#### **Как получить API-ключи?**

API-ключи можно:\
✅ Зарегистрировать самостоятельно в консоли разработчика Google.\
✅ Приобрести готовые ключи – это удобнее и проще, особенно если требуется большой объём данных.

#### **Лимиты API-ключей**

Примерные лимиты:\
✅ **5 поисковых запросов** – парсинг поисковой выдачи.\
✅ **10 000 видео** – парсинг информации о видео.\
✅ **10 000 каналов** – парсинг информации о каналах.

💡 **Важно!**\
Квота общая для всех методов и заданий парсинга! Если ключ полностью израсходован, то никакие другие запросы выполнить нельзя, пока квота не обновится.

### 8\. Прокси для парсинга через InnerTube API

При использовании метода парсинга InnerTube API могут понадобиться **прокси**, так как YouTube ограничивает частоту запросов. При слишком большом объёме обращений сервис может запросить прохождение ReCaptcha для защиты от автоматизированных систем.

#### Какие прокси лучше использовать?

**Рекомендуются:**

✅ Индивидуальные IPv4-прокси с высокой скоростью и низким пингом (серверные, резидентные, мобильные).

**Не рекомендуется:**

❌ IPv6-прокси – YouTube часто их блокирует.

❌ Публичные прокси – низкая скорость, нестабильность, высокая вероятность попадания под ограничения.

#### Лимиты запросов для одного IP

Примерные лимиты:\
✅ **50 поисковых запросов** – парсинг поисковой выдачи.\
✅ **500 – 1000 видео** – парсинг информации о видео.\
✅ **500 – 1000 каналов** – парсинг информации о каналах.

💡 **Важно!**\
Использование **качественных прокси** позволяет увеличить лимиты и снизить вероятность блокировки.