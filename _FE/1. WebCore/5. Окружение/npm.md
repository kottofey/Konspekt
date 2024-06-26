Node Package Manager
Это нечто вроде brew или aptitude.

Состоит из двух частей:

- CLI (интерфейс командной строки) – средство для размещения и скачивания пакетов,
- онлайн-репозитории - содержащие JS пакеты.

#вставитьОглавление
# 1. Что такое NPM
## package.json
Это файл описание и настройки JS-проекта. Можно инициализировать проект, запустив команду `npm init` в корне проекта. Создастся шаблонный `package.json` со следующими полями:
- name
- version
- description
- entry point (main)
- test command
- git repository (url)
- keywords
- author
- license
```json
{
  "name": "testNpm",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/kottofey/testNpmRepo"
  },
  "author": "kottofey <romeokontakt@yandex.ru>",
  "license": "ISC",
  "description": "This is a test NPM project"
}
```
## Скрипты npm
Поле `scripts` - это объект, содержащий поля-скрипты для автоматизации сборки. Ключи полей нужны для вызова этих скриптов. Например:
```json
{
  "scripts": {
    "build": "tsc",
    "format": "prettier --write **/*.ts",
    "format-check": "prettier --check **/*.ts",
    "lint": "eslint src/**/*.ts",
    "pack": "ncc build",
    "test": "jest",
    "all": "npm run build && npm run format && npm run lint && npm run pack && npm test"
  }
}
```

`npm run build` - запустит упаковщик `tsc`
`npm run lint` - запустит линтер
и т д

Модули (например, `eslint`, `prettier`, `ncc`, `jest`), использующиеся в скриптах могут быть установлены локально для проекта (внутри `node_modules/.bin/`) или глобально.

## Dependencies и devDependencies
Они представляют собой словари с именами npm-библиотек (ключ) и их версиями (значение)

Эти зависимости устанавливаются следующим образом:
`npm install --save module_name` - установка глобально, для использования в продакшене
`npm install --save-dev module_name` - установка только для разработки. Также, `--save-dev` эквивалентно ключу `-D`

`Dependecies` — это зависимости, от которых напрямую зависит работа проекта, при удалении хотя бы одного из них произойдёт бада-бум. А может и большой биг-бада-бум.

`Dev-dependencies` — вспомогательные зависимости, которые нужны для разработки. Например, линтер, упаковщик и т д.

### Версии зависимостей
В файле package.json в разделе зависимостей перед версией могут стоять следующие символы:
- `^`: установит последний минорный релиз. Например, `^1.0.4` установит версию `1.3.0`, если это последний минорный релиз в серии `1` мажорного релиза
- `~`: последний патч-релиз. `~1.0.4` установит `1.0.7`, если эта последняя минорная версия в серии минорных релизов `1.0`
- `*`: установит абсолютно все апдейты, включая и мажорные версии
- Если удалить символ возле версии пакета, то он обновляться не будет вообще.

Если обобщить, то `^` позволит обновлять до минорных версий, а `~` обновит только патчи, без минорных версий

Все версии пакетов будут отображены в сгенерированном файле `package-lock.json`

## Файл package-lock.json
Файл `package-lock.json` описывает версии пакетов, используемые в текущем JS-проекте, которые находятся в папке `node_modules`.

`Package-lock.json` нужен для того, чтобы на разных машинах можно было установить одинаковый набор модулей с одинаковыми версиями. Это можно сделать, запустив `npm install`, зайдя в папку с проектом.

Хорошим делом будет закоммитить этот файл в репозиторий. 
# 2. Работа с пакетами
## Установка пакетов
`npm install` – команда, устанавливающая пакеты.

По умолчанию `npm install <package-name>` со знаком `^` установит последнюю версию пакета. `npm install` скачает пакет в папку проекта `node_modules` в соответствии с конфигурацией в файле `package.json`, обновив версию пакета везде, где это возможно (и, в свою очередь, обновив `package-lock.json`).
### Флаги

- `-g` - установка пакета глобально
- `--production` - установятся только нужные для работы приложения зависимости из `dependencies`, не раздувая `node_modules`
- `-D` или `--save-dev` - устанавливает пакет в раздел devDependencies
- `-E` или `--save-exact` - фиксирует версию пакета и не обновляет её. То есть, в файле `package.json` убираются префиксы из версии пакета
## Удаление пакетов
`npm remove` / `npm r` / `npm uninstall` / `npm un` - удаление пакетов

## Чистая установка
`npm ci` - (*clean install*) предварительно очистит папку node_modules и установит пакеты в точном соответствии с файлом `package-lock.json`, версии будут использоваться именно из лок-файла, чтобы в точности скопировать структуру проекта.

## Аудит пакетов
Чтобы избежать добавления в репозитории вредоносных пакетов, организация npm.js пришла к идее аудита экосистемы, создав модуль `npm audit`. Он предоставляет информацию об уязвимостях в пакетах и о существовании версий с исправлениями.

Если исправления доступны в следующих версиях пакета, `npm audit fix` автоматически обновит версии затронутых зависимостей.

## Публикация своего пакета
Отправить пакет в npmjs.com очень просто – нужно набрать в консоли `npm publish`

Важная часть, которой пренебрегают авторы – версионирование или семантическое версионирование. Вот набор эмпирические правил semver.org, указывающих, когда следует увеличить номер версии:

- ***Мажорная версия:*** когда сделаны обратно несовместимые изменения API.
- ***Минорная версия:*** когда вы добавляете новую функциональность, не нарушая обратной совместимости.
- ***Патч-версия:*** когда вы делаете обратно совместимые исправления.

Еще более важно следовать вышеуказанным правилам при публикации собственных пакетов, чтобы гарантировать, что вы не нарушаете чью-либо совместимость, так как по умолчанию в npm берется версия `^` (следующая младшая версия).