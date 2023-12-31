# Домашнее задание к занятию "Репликация и масштабирование. Часть 2" - `Хамов Олег`

### Задание 1

1. активный master-сервер и пассивный репликационный slave-сервер;

    При таком горизонтальном масштибировании у нас есть сервер для внесения,

    редактирования данных и копия сервера, которую можно использовать для чтения

    данных. Так как у нас всего два сервера то получаем простую настройку и минимальную

    нагрузку на сеть и безопасность данных, так как есть копия в виде slave-сервера.

2. master-сервер и несколько slave-серверов;

    Преимущество этого типа репликации в том, что мы можем использовать более

    одного Slave сервера. Обычно следует использовать не более 20 Slave серверов при работе

    с одним Master. Тогда приложение выбирает случайным образом один из Slave серверов

    для обработки запросов. Повышает количество запросов на чтение данных, но

    увеличивает нагрузку на мастер-сервер. Намного чаще репликацию Master-

    Slave используют не для масштабирования, а для резервирования. В этом

    случае, Master сервер обрабатывает все запросы от приложения. Slave сервер работает в

    пассивном режиме. Но в случае выхода из строя Master, все операции переключаются на Slave.

3. активный сервер со специальным механизмом репликации — distributed replicated block device (DRBD);

    DRBD (Distributed Replicated Block Device — распределённое реплицируемое блочное

    устройство) представляет собой распределенное, гибкое и универсально реплицируемое

    решение хранения данных для Linux. Оно отражает содержимое блочных устройств, таких

    как жесткие диски, разделы, логические тома и т.д. между серверами. Оно создает копии

    данных на двух устройствах хранения для того, чтобы в случае сбоя одного из них можно

    было использовать данные на втором. Преимущество, таким образом, в том, что

    повышается отказоустойчивость, за счет копий данных сервера на другом сервере.

4. SAN-кластер.

    В контексте технологии SAN, кластеризация серверов подразумевает объединение

    нескольких серверов с целью увеличения производительности и/или надежности.

    Серверы могут кластеризоваться и вне SAN окружения, но существует несколько

    преимуществ кластеризации внутри SAN. Среди них: разделяемый доступ к дискам и

    ленточным устройствам, большая производительность репликации данных, лучшая

    масштабируемость дисковой системы и расширенная отказоустойчивость.

    Кластеризация серверов может быть незаменима в случае, когда необходимо обеспечить

    100% отказоустойчивость. В этом случае можно объединить серверы через глобальные

    сети для обеспечения необходимого расстояния между серверами. При этом, эти сервера

    могут быть так же подключены к локальной SAN, а локальная SAN может включать

    дополнительные кластеры.

    Архитектура SAN так же обеспечивает возможность безболезненного роста. Техника

    управления емкостью хранилищ данных может быть использована, что бы обеспечить

    постоянное ее (емкости) увеличение, по мере необходимости. Если необходимо

    увеличение вычислительной мощности, SAN позволяет добавлять новые серверы таким

    образом, что они будут иметь разделяемый доступ к данным. Для увеличения скорости

    доступа к данным, могут быть созданы несколько их копий, это позволяет преодолеть

    ограничение производительности одного диска.

### Задание 2

1) Мы можем разбить общую базу данных на отдельные базы данных - DB Users, DB Books, DB Stores - это будет вертикальный шардинг, 

2) вторым шагом мы можем, например, большую базу данных с пользователями разбить на 2 сервера (горизонтальный шардинг)

и на 1 сервере оставить id, имя, пароль, почту, адрес, телефон на другом сервере будем хранить историю заказов, посещения, любимые категории, избранные книги, доступ к книгам онлайн.

3) Два сервера будут работать как master-сервера, для повышения производительности можно к первому серверу добавить slave-сервер.

![block-shema.png](https://github.com/oleghamov/Replik-Mashtab.2-12-07-16-11-23-hw-/blob/master/block-shema.png)`


