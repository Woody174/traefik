# Прокси сервер

## 1. Клонировать репозиторий и зайти в него

```text
git clone https://github.com/Woody174/traefik.git

cd traefik
```

## 2. Создать файл `acme.json` и изменить права на файл

> В файле будут храниться все сертификаты Let's Encrypt

```console
touch acme.json

chmod 600 acme.json
```

## 3. Заполняем переменные окружения
```console
cp .env.example .env
```
Указываем Email для сертификатов Let's Encrypt

## 4. Создаем Docker сеть
```console
docker network create proxy
```

## 5. Запускаем контейнер
```console
docker compose up -d
```

___

## Добавление хостов

В файле `compose.yml` добавить следущие строки, заменив <ROUTE_NAME>, <HOST_NAME> на свои названия:

```text
services:
    container:
    
        ....

        networks:
            - proxy
        labels:
            - "traefik.enable=true"
            - "traefik.http.routers.<ROUTE_NAME>.entrypoints=websecure"
            - "traefik.http.routers.<ROUTE_NAME>.rule=Host(`<HOST_NAME>`)"

networks:
  proxy:
    external: true
```
