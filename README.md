# Docker под 1C Bitrix проекты

## Установка docker и docker-compose
https://docs.docker.com/install/

## Разворачивание чистого проекта 
1. Склонировать репозиторий
2. Запустить команду 
```bash
make up
```

## Разворачивание существующего проекта
1. Склонировать репозиторий
2. Отредактируйте переменные в `Makefile` 
    - `MYSQL_DUMP`: путь до sql файла
    - `RSYNC_ROOT`: путь до корневой директории production
4. Запустить команду
```bash
make init
```

## Команды
- Иницилизация проекта 
```bash
make init
```

- Запуск контейнеров 
```bash
make up
```

- Остановка контейнеров
```bash
make down
```

- Восстановление БД
```bash
make restore-mysql
```
