# Домашнее задание к занятию 1. «Типы и структура СУБД»
## Введение
Перед выполнением задания вы можете ознакомиться с [дополнительными материалами](https://github.com/netology-code/virt-homeworks/tree/virt-11/additional).

## Задача 1
Архитектор ПО решил проконсультироваться у вас, какой тип БД лучше выбрать для хранения определённых данных. 

Он вам предоставил следующие типы сущностей, которые нужно будет хранить в БД:
- электронные чеки в json-виде,
- склады и автомобильные дороги для логистической компании,
- генеалогические деревья,- кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации,
- отношения клиент-покупка для интернет-магазина.
Выберите подходящие типы СУБД для каждой сущности и объясните свой выбор.

## Задача 2
Вы создали распределённое высоконагруженное приложение и хотите классифицировать его согласно CAP-теореме. Какой классификации по CAP-теореме соответствует ваша система, если (каждый пункт — это отдельная реализация вашей системы и для каждого пункта нужно привести классификацию):
- данные записываются на все узлы с задержкой до часа (асинхронная запись);
- при сетевых сбоях система может разделиться на 2 раздельных кластера;
- система может не прислать корректный ответ или сбросить соединение.
Согласно PACELC-теореме как бы вы классифицировали эти реализации?

## Задача 3
Могут ли в одной системе сочетаться принципы BASE и ACID? Почему?

## Задача 4
Вам дали задачу написать системное решение, основой которого бы послужили:
- фиксация некоторых значений с временем жизни,
- реакция на истечение таймаута.
Вы слышали о key-value-хранилище, которое имеет механизм Pub/Sub. Что это за система? Какие минусы выбора этой системы?

 ## Ответ 1:

- Электронные чеки в json-виде;
Для хранения этой сущности могла бы подойти документоориентированная NoSQL DB, такая как MongoDB. Это СУБД была изначально разработана в ключе хранения любого набора данных без четкой привязки и отношений.

- Склады и автомобильные дороги для логистической компании;
Вероятно, здесь можно было бы задействовать графовую СУБД. Когда есть точки (склады) и отношения (ребра) между ними.

- Генеалогические деревья;
В эту концепцию отлично ложится иерархическая БД. Когда у каждого потомка есть определенный родитель.

- Кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации;
Все, что касается кэширования, быстродействия, ограниченного времени жизни, должно использовать in-memory БД, такие как memcached или reddis.

- Отношения клиент-покупка для интернет-магазина;
Когда идет речь об отношениях между различными данными, лучше реляционных БД не найти. Они логичны, структурированы, имеют определенные типы данных и схемы размещения этих данных.

## Ответ 2: 

Например:

- Данные записываются на все узлы с задержкой до часа (асинхронная запись);

По PACELC это система класса PA/EC.
По CAP: РА

- При сетевых сбоях система может разделиться на 2 раздельных кластера;

По PACELC это система класса PA/EL.
По CAP: РА

- Система может не прислать корректный ответ или сбросить соединение;

По PACELC это система класса PC/EL.
По CAP: РС

## Ответ 3:

Согласно классификации САР, БД могут быть либо больше ACID, либо больше BASE. Одновременное присутствие принципов ACID и BASE в равных пропорциях в системах недопустимо.

## Ответ 4: 

Это система типа in-memory DB. NoSQL БД типа BASE, хранящая данные в оперативной памяти сервера.
Из минусов использования:
- Реакция на истечение таймаута может быть фатальной для определенных данных;
- Не всегда есть возможность сбросить данные из памяти на диск;
- Редис работает в один поток, что ограничивает задействование свободного пула ресурсов сервера.
