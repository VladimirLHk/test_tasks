# Шаблон для AmoCRM виджетов.

## Начало

Скачать репозиторий как архив и распаковать в любом месте.

Сменить название папки custom-name

Инициализировать git - `git init`

Добавить удаленный репозиторий который выдан под разработку виджета.


## Разработка
Для начала необходимо создать тестовый аккаунт в амо. Зайти в настройки, Api, добавить виджет, указать уникальный код виджета `code`.
В ответ получить `secret_key` и указать их в manifest.json.

### Локальный сервер
Для разработки лучше всего использовать локальный сервер, запуск производится:
```
cd server
node server.js
```
^ {{widget.name}} - название папки с виджетом (alarmplan_tc, pandora, disabled_responsible_user)

Перед тестированием перейти по адресу https://localhost:8080/{{widget.name}}/src/index.js, чтоб принять протухший ssl сертификат.

В script.js виджета указать:
```javascript
define(['https://localhost:8080/{{widget.name}}/src/index.js?v='+Math.random()], function (widget) {
     return widget;
});
```

Перейти в папку с виджетом `cd {{widget.name}}`, установить зависимости `yarn`, собрать zip архив `yarn gulp`.
Получившийся widget.zip загрузить на странице Настройки, Api.


Далее зайти в интеграции, и активировать виджет (иногда требуется 5-10 минут после заливки виджета, чтоб он нормально отображался и активировался)

Далее виджет должен инициализироваться там где ему положено, с локального сервера. Можно спокойно править ./src/index.js


## Сборка продакшен версии

Перед компиляцией билда для продакшена в script.js указать:
```javascript
define(['./src/index.js'], function (widget) {
  return widget;
});
```
Также в manifest.json указать `code`, `secret_key` и `version` для продакшен версии.

Собрать zip архив `yarn gulp` и залить его на странице настроек, затем активировать в интеграциях и протестировать.

## Если есть бага в репозитории

* Клонируйте этот репозиторий
* Создайте новую ветку
* Исправляйте в ней баг и тп 
* Создайте pull-request в master 
* В описание pull опишите что было исправлено