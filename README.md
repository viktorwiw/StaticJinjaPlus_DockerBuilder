# StaticJinjaPlus_DockerBuilder

Готовые Docker-образы и инструменты для сборки кастомных версий StaticJinjaPlus - статического генератора сайтов на Jinja2.


## Запуск контейнера

Если еще не установлен Docker, [установите егo](https://hub.docker.com/r/wiwikin/static-jinja-plus)

Выберите нужный (образ)[https://hub.docker.com/r/wiwikin/static-jinja-plus] 

Запустите контейнер

```
docker run --rm -v $(pwd)/{TEMPLATES_PATH}:/app/templates -v $(pwd)/{BUILD_PATH}:/app/build wiwikin/static-jinja-plus:${TAG}
```

``${TEMPLATES_PATH}`` - путь к каталогу с вашими html-шаблонами
``${BUILD_PATH}`` - путь к каталогу, где будут созданы отрендеренные HTML-страницы
``${TAG}`` - тег образа


## Сборка своего образа

### Получение хеша для скачивания [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus)

Для всех версий, кроме latest, develop, slim и develop_clim необходимо получить хэш-сумму:

```
curl -sL https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${SJP_TAG}.tar.gz | sha256sum
```

${JSP_TAG} - тег в репозитории [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus).

### Сборка образов

Для сборки версий: latest, develop, slim и develop_clim 

```docker
docker build -t ${docker_username}/${image_name}:${TAG} -f ${DOCKERFILE} . 
```

Для сборки версий: 0.1.0, 0.1.1, 0.1.0-slim, 0.1.1-slim

```docker
docker build -t ${docker_username}/${image_name}:${TAG} -f ${DOCKERFILE} . --build-arg SJP_TAG=${SJP_TAG} --build-arg SJP_HASH=${SJP_HASH}
```

``${docker_username}`` - имя пользователя Docker
``${image_name}`` - имя образа
``${TAG}`` - тег образа
``${DOCKERFILE}`` - путь к Dockerfile
``${SJP_TAG}`` - тег из репозитория [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus)
``${SJP_HASH}`` - хэш сумма

### Примеры команд для сборки

Скачайте проект и перейдите в корень проекта, выполните одну из команд:

#### ubuntu  - на базе [ubuntu](https://hub.docker.com/_/ubuntu)

- latest - Последняя стабильная версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus)

```docker
docker build -t wiwikin/static-jinja-plus:latest -f ubuntu/0.1/Dockerfile .
```

- develop - Версия последний коммит из ветки main [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 

```docker
docker build -t wiwikin/static-jinja-plus:develop -f ubuntu/develop/Dockerfile .
```

- 0.1.0 - Версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 0.1.0

```docker
docker build -t wiwikin/static-jinja-plus:0.1.0 -f ubuntu/0.1/Dockerfile . --build-arg SJP_TAG=0.1.0 --build-arg SJP_HASH=3555bcfd670e134e8360ad934cb5bad1bbe2a7dad24ba7cafa0a3bb8b23c6444
```

- 0.1.1 - Версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 0.1.1

```docker
docker build -t wiwikin/static-jinja-plus:0.1.1 -f ubuntu/0.1/Dockerfile . --build-arg SJP_TAG=0.1.1 --build-arg SJP_HASH=30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b
```

#### На базе [python-slim])(https://hub.docker.com/_/python)

- 0.1.0-slim - Версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 0.1.0

```docker
docker build -t wiwikin/static-jinja-plus:0.1.0-slim -f python/0.1/Dockerfile . --build-arg SJP_TAG=0.1.0 --build-arg SJP_HASH=3555bcfd670e134e8360ad934cb5bad1bbe2a7dad24ba7cafa0a3bb8b23c6444
```

- 0.1.1-slim - Версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 0.1.1

```docker
docker build -t wiwikin/static-jinja-plus:0.1.1-slim -f python/0.1/Dockerfile . --build-arg SJP_TAG=0.1.1 --build-arg SJP_HASH=30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b
```

- develop-slim - Версия последний коммит из ветки main [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) 

```docker
docker build -t wiwikin/static-jinja-plus:develop-slim -f python/develop/Dockerfile .
```

- slim - Последняя стабильная версия [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus)

```docker
docker build -t wiwikin/static-jinja-plus:slim -f python/0.1/Dockerfile .
```
