Можно пробросить папку или файлы внутрь контейнера, чтобы динамически их обновлять.

Формат: `src:dest`:
- `src`: путь относительно файла docker-compose.yml
- `dest`: абсолютный путь внутри контейнера

Пример файла `docker-compose.yml`:

```docker
networks:
  eom:

volumes:
  db:

services:
  backend:
    depends_on:
      - db
    restart: unless-stopped
    ports:
      - "8891:8891"
    build:
      context: ./backend
    networks:
      - eom
    volumes:
#   относительный путь относительно файла docker-compose.yml:абсолютный путь внутри контейнера
      - ./backend/src:/usr/src/app/src/
      - ./backend/.env:/usr/src/app/.env

  frontend:
    restart: unless-stopped
    ports:
      - "8890:8890"
    build:
      context: ./frontend
    volumes:
      #   относительный путь относительно файла docker-compose.yml:абсолютный путь внутри контейнера
      - ./frontend/src:/usr/src/app/src/
      - ./frontend/.env/:/usr/src/app/.env/
    networks:
      - eom

  db:
    networks:
      - eom
    image: mysql:8
    restart: unless-stopped
    environment:
      - MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD
      - MYSQL_DATABASE=$MYSQL_DATABASE
    ports:
      - $MYSQLDB_LOCAL_PORT:$MYSQLDB_DOCKER_PORT
    volumes:
      - db:/var/lib/mysql

```