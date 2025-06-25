# Удаление ненужных и неиспользуемых образов

`docker system prune`

# Остановка mysql контейнера

```sh
mysql -h 127.0.0.1 -P 3308 -u root -p root
```

Порт '3308' заменить на тот, который расшарен из контейнера

После этого в mysql `shutdown;`

# Приколы с часовыми поясами
В контейнерах по-умолчанию установлено время UTC. В связи с чем время может обрабатываться некорректно, нужно в докер-файле явно указывать часовой пояс. Пример:

```docker
FROM node:lts-alpine

ENV TZ=Europe/Moscow

LABEL authors="kottofey"

WORKDIR /usr/src/app

COPY package*.json .

RUN npm install

COPY . .

EXPOSE 8891

#CMD [ "node", "--env-file=.env", "src/express/bin/www.ts" ]
CMD [ "./start-express" ]

```