# Changelog

Все значимые изменения проекта документируются в этом файле.

Формат основан на [Keep a Changelog](https://keepachangelog.com/ru/1.1.0/), версионирование следует [Semantic Versioning](https://semver.org/lang/ru/).

## [Unreleased]

### Added
- Инициализирован Go-модуль `github.com/physicist2018/mopsmap-rest` (Go 1.24)
- Создана структура каталогов: `cmd/`, `internal/`, `pkg/`
- Добавлен Dockerfile для сборки контейнера с MOPSMAP на базе Alpine Linux
- Включены исходники MOPSMAP на Fortran 2008 (28 файлов `.f90`) в `docker/mopsmap/src/`
- Включены файлы данных MOPSMAP (рефракционные индексы, длины волн) в `docker/mopsmap/data/`
- Включены вспомогательные Python-скрипты и примеры в `docker/mopsmap/misc/`
- Добавлено руководство пользователя MOPSMAP в `docker/mopsmap/doc/`
- Добавлен `.gitignore` для Go-проекта
- Добавлены лицензионные файлы: GPL v2 (проект), GPL v3 (MOPSMAP)
- Добавлен README.md с описанием проекта
- Добавлен CHANGELOG.md

## [0.1.0] — не выпущено

Начальная стадия проекта. REST API пока не реализован.
