# Labaratory work III
Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере CMake.
# Progress of work
Перед началом выполнения лабораторной работы рекомендую заранее настроить рабочее пространство. Для этого необходимо как минимум копировать репозиторий с помощью ```git clone```, а также воспользоваться командами ```alias ...``` и ```export ...``` для работы с редактором и переменными соответственно.

```bash
$ git clone https://github.com/tp-labs/lab03.git
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GIST_TOKEN=<сохраненный_токен>
$ alias edit=<nano|vi|vim|subl>
```

Затем приступаем к выполнению непосредственно самой работы. По ходу работы я буду давать необходимые уточнения и комментарии. Я сознательно решил не делить выполнение на 3 "стадии", как это указано в репозитории с [заданием](https://github.com/tp-labs/lab03) на GitHub. Некоторые пункты бы содержали слишком мало информации, чтобы выделять это как отдельную задачую Поэтому выполняем все последовательно и по порядку.

```bash
$ cd lab03
$ ls
CMakeLists.txt    formatter_lib            LICENSE      README.md           solver_lib
formatter_ex_lib  hello_world_application  preview.png  solver_application
```
Удостоверимся в правильности и целостности скопированного репозитория. Для этого с помощью команды ```cd ...``` перейдем в репозиторий и пропишем команду ```ls``` без аргументов. Затем приступим к изменению/добавлению CMakeLists.txt файлов. Корневой такой файл уже существует, но в конце нам нужно будет его отредактировать. Вначале добавим новые файлы в каждую из директорий.

Чтобы не прописывать постоянно команду ```cd ...```, будем использовать редактор и команду ```nano ...``` (```edit ...``` усли проводилась настройка рабочего просмтранства) с указанием где нужно создать файл CMakeLists.txt. Также можно использовать команду ```cat >> ...``` как указано в [Tutorial](https://github.com/tp-labs/lab03). Мне она кажется не совсем удобной, поэтому временно откажемся от ее использования. Перейдем к созданию файлов.

## formatter_lib/CMakeLists.txt

```bash
$ nano formatter_lib/CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(formatter)

add_library(formatter STATIC formatter.cpp)

target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

## formatter_ex_lib/CMakeLists.txt

```bash
$ nano formatter_ex_lib/CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(formatter_ex)

add_library(formatter_ex STATIC formatter_ex.cpp)

target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex formatter)
```

## solver_lib/CMakeLists.txt

```bash
$ nano solver_lib/CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(solver)

add_library(solver STATIC solver.cpp)

target_include_directories(solver PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

## hello_world_application/CMakeLists.txtformatter_lib/CMakeLists.txt

```bash
$ nano hello_world_application/CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(hello_world)

add_executable(hello_world hello_world.cpp)

target_link_libraries(hello_world formatter_ex)
```

## solver_application/CMakeLists.txt

```bash
$ nano solver_application/CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(solver_app)

add_executable(solver equation.cpp)

target_link_libraries(solver formatter_ex solver)
```

Добавив везде по CMakeLists.txt перейдем в корневую папку "lab03" и изменим исходеый файл CMakeLists.txt

## Корневой CMakeLists.txt (работаем в lab03)

```bash
$ nano CMakeLists.txt
```
```text
cmake_minimum_required(VERSION 3.4)
project(lab03)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)

add_subdirectory(hello_world_application)
add_subdirectory(solver_application)
```
