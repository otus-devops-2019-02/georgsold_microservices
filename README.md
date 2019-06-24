# georgsold_microservices
georgsold microservices repository


Docker compose по умолчанию задает имя проекту равное названию каталога с компоновочным файлом. Изменить это можно задав ключ -p или определив переменную COMPOSE_PROJECT_NAME. Можно задать имя в ямле, как имя контейнера, но имхо через переменную правильнее.

Звездочка:

Если не выполнять сборку, то код каким-то образом то должен появиться ) Вариант: примонтировать через опцию volumes код из директорий /app/ui, /app/post-py и /app/comment в /app. Обновленный код нужно скопировать на docker host ручками/скриптом/прописать в конфе или монтировать с локали.


Итогвый образ после оптимизиций - в dockerfile.
Описание dockerfile более менее наглядно (для эксперимента - прошу коллегу по работе сделать мне типа ревью :) ).
Сборка:
docker build -t georgsold/post:2.0 src/post-py

Остальные по аналогии.

Стартуем:
docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db --name=post_db -v reddit_db:/data/db mongo:latest
docker run -d --network=reddit --network-alias=post --name=post georgsold/post:2.0
docker run -d --network=reddit --network-alias=comment --name=comment georgsold/comment:2.0
docker run -d --network=reddit -p 9292:9292 --name=ui georgsold/ui:3.0

В данном случае для монги подключен созданный по домашке вольюм.
