# DSlipPortable
# Установка Boost используя vcpkg
Команда для поиска расположения vcpkg
```
Get-Command vcpkg -ErrorAction SilentlyContinue | Select-Object Source
```
Данная команда нам выведет путь распложения vcpkg, после чего по этому пути надо перейти
```
cd "C:\Program Files\vcpkg" 
```
После перехода по пути при наличии пакетов boost (в моём случае попытки установки предпринимались ранее) следует удалить ошибочные файлы
```
.\vcpkg remove boost-filesystem boost-system boost-program-options --recurse
```
> Команда --recurse нужна для очистки уже сущесвующих файлов библиотек что бы не было дублирования, соответственно если установка идёт впервые, то данную команду необходимо убрать

Также во избежание проблем следует очистить кеш сборки
```
Remove-Item -Recurse -Force C:\Program Files\vcpkg\buildtrees\boost-* -ErrorAction SilentlyContinue 
```
А теперь переходим к самой установки boost со всеми зависимостями. В нашем случае необходимы следующие библиотеки ```date_time system program_options```
В любом случае если чего то не будет хватать, то это можно спокойно доустановить.

```
.\vcpkg install boost-system:x64-windows boost-filesystem:x64-windows boost-program-options:x64-windows boost-date-time:x64-windows
```
> Стоит учитывать что при установки данных библиотек к ним добавятся созависмые. Для наглядного примера можно вызвать команду ```vcpkg list boost``` в командной строке

```
C:\Program Files\vcpkg\installed\x64-windows\include\spdlog>vcpkg list boost
boost-algorithm:x64-windows                       1.90.0#1            Boost algorithm module
boost-align:x64-windows                           1.90.0#1            Boost align module
boost-any:x64-windows                             1.90.0#1            Boost any module
boost-array:x64-windows                           1.90.0#1            Boost array module
boost-asio:x64-windows                            1.90.0#1            Boost asio module
boost-asio[deadline-timer]:x64-windows                                Build with deadline_timer support
boost-asio[spawn]:x64-windows                                         Build with spawn (stackful coroutines) support
boost-assert:x64-windows                          1.90.0#1            Boost assert module
boost-atomic:x64-windows                          1.90.0#1            Boost atomic module
boost-bind:x64-windows                            1.90.0#1            Boost bind module
boost-chrono:x64-windows                          1.90.0#1            Boost chrono module
boost-cmake:x64-windows                           1.90.0#1            Boost cmake module
boost-concept-check:x64-windows                   1.90.0#1            Boost concept_check module
boost-config:x64-windows                          1.90.0#1            Boost config module
boost-container-hash:x64-windows                  1.90.0#1            Boost container_hash module
boost-container:x64-windows                       1.90.0#1            Boost container module
boost-context:x64-windows                         1.90.0#1            Boost context module
boost-conversion:x64-windows                      1.90.0#1            Boost conversion module
boost-core:x64-windows                            1.90.0#1            Boost core module
boost-date-time:x64-windows                       1.90.0#1            Boost date_time module
boost-describe:x64-windows                        1.90.0#1            Boost describe module
boost-detail:x64-windows                          1.90.0#1            Boost detail module
boost-endian:x64-windows                          1.90.0#1            Boost endian module
boost-exception:x64-windows                       1.90.0#1            Boost exception module
boost-filesystem:x64-windows                      1.90.0#1            Boost filesystem module
boost-function-types:x64-windows                  1.90.0#1            Boost function_types module
boost-function:x64-windows                        1.90.0#1            Boost function module
boost-functional:x64-windows                      1.90.0#1            Boost functional module
boost-fusion:x64-windows                          1.90.0#1            Boost fusion module
boost-headers:x64-windows                         1.90.0#1            Boost headers module
boost-integer:x64-windows                         1.90.0#1            Boost integer module
boost-intrusive:x64-windows                       1.90.0#1            Boost intrusive module
boost-io:x64-windows                              1.90.0#1            Boost io module
boost-iterator:x64-windows                        1.90.0#1            Boost iterator module
boost-lexical-cast:x64-windows                    1.90.0#1            Boost lexical_cast module
boost-move:x64-windows                            1.90.0#1            Boost move module
.........................и так далее
```
> Команда ```vcpkg list boost``` позволяет просмотреть какая команда установки была выбрана.

Также задачей была установка библиотеки ```spdlog```

```
.\vcpkg install spdlog:x64-windows
```
