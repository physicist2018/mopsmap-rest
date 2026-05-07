# mopsmap-rest

REST API для [MOPSMAP](https://mopsmap.net) — программы расчёта оптических свойств аэрозольных частиц.

## Что такое MOPSMAP

MOPSMAP (Modeled Optical Properties of ensembles of aerosol Particles) — научная программа на Fortran 2008, разработанная Йозефом Гаштайгером (University Vienna, LMU Munich). Она вычисляет:

- Оптические свойства аэрозолей (коэффициенты рассеяния, поглощения, ослабления)
- Фазовые функции
- Матрицы рассеяния
- Лидарные отношения

для ансамблей частиц с учётом размера, формы, состава, длины волны и относительной влажности. Входные данные задаются текстовым файлом, результат выдаётся в форматах ASCII и NetCDF.

## Цель проекта

Обернуть консольную Fortran-программу MOPSMAP в REST API на Go, чтобы:

- Принимать входные параметры через HTTP-запросы
- Запускать MOPSMAP как subprocess
- Парсить и отдавать результаты в JSON
- Работать в Docker-контейнере (включая скомпилированную Fortran-программу)

## Структура проекта

```
mopsmap-rest/
├── cmd/                  # Точка входа Go-приложения (в разработке)
├── internal/             # Внутренние пакеты (в разработке)
├── pkg/                  # Переиспользуемые пакеты (в разработке)
├── docker/
│   ├── Dockerfile        # Сборка Docker-образа
│   ├── mopsmap/          # Исходники MOPSMAP на Fortran
│   │   ├── src/          # 28 файлов .f90
│   │   ├── data/         # Данные (рефракционные индексы, длины волн и пр.)
│   │   ├── doc/          # Руководство пользователя (PDF)
│   │   ├── misc/         # Python-скрипты, примеры, libRadtran
│   │   └── Makefile      # Верхнеуровневый Makefile
│   └── mopsmap_program_v1.0.tar.gz  # Архив с программой
├── go.mod                # Go-модуль
├── go.sum
├── LICENSE               # GPL v2
├── CHANGELOG.md
└── README.md
```

## Зависимости

### Go

- Go 1.24+

### Fortran (MOPSMAP)

- gfortran
- NetCDF-Fortran (libnetcdff)

## Сборка и запуск

### Локально

```sh
# Собрать Fortran-программу
cd docker/mopsmap
make

# Запустить MOPSMAP напрямую
./mopsmap путь/к/input.txt
```

### Docker

```sh
# Собрать образ
docker build -t mopsmap-rest docker/

# Запустить контейнер
docker run mopsmap-rest
```

## Пример входного файла MOPSMAP

```text
mode 1 size log_normal 0.1 2.0 1 0.005 20
mode 1 refrac 1.52 0.01
mode 1 shape spheroid oblate 1.7
mode 1 kappa 0.5
mode 1 density 2
rH 70
size_equ cs
output num_theta 4
wavelength range 0.4 0.5 0.1
output integrated
output phase_function
scatlib '../optical_dataset'
```

## Лицензия

- **mopsmap-rest** — GNU General Public License v2 (см. [LICENSE](LICENSE))
- **MOPSMAP** — GNU General Public License v3 (см. [docker/mopsmap/COPYING](docker/mopsmap/COPYING))

## Ссылки

- [Официальный сайт MOPSMAP](https://mopsmap.net)
- [MOPSMAP на GitHub](https://github.com/physicist2018/mopsmap-rest)
