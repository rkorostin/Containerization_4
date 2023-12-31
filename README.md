
# Dockerfile и слои

## Дома необходимо собрать образ и запустить из него контейнер: Основой образа должна быть alpine. Установить необходимо mariaDB. Также не забудьте об уменьшении размера образа. Способ обсуждался на лекции. Необходимо открыть порт для коммуникации с другими сущностями. Для проверки решения необходимо подключить к такому контейнеру phpmyadmin. Необходимо, чтобы в нем вы увидели данные из вашей БД. Также при запуске необходимо смонтировать внешнюю папку для хранения данных БД вне контейнера.


1. Создание Dockerfile
```
vi Dockerfile
```
Внутри файла добавим следующие инструкции:
### Основой образ
FROM alpine
### Установка MariaDB и уменьшение размера
RUN apk add mariadb mariadb-client && rm -rf /var/cache/apk/*
### Открытие порта
EXPOSE 3306
### Создание директории для данных БД
RUN mkdir /data
### Запуск MariaDB
CMD ["mysqld", "--datadir=/data"]

2. Сборка образа Docker
```
docker build -t gb-hw4 .
```
3. Запуск контейнера
```
docker run -d -p 3306:3306 -v /media/data:/data --name hw4-mariadb-container gb-wh4
```
4. Подключение phpmyadmin
```
docker run -d -p 8080:80 --link hw4-mariadb-container:db phpmyadmin/phpmyadmin
```

