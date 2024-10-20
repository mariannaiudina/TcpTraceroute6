# TcpTraceroute6
TcpTraceroute6 — это утилита для анализа маршрутизации IPv6. Она использует протокол TCP для выполнения трассировки пути между двумя узлами сети и позволяет отслеживать путь пакета данных от источника до места назначения, показывая все промежуточные хосты и их IP-адреса.
## Основные функции
### 1. Трассировка пути
Основная функция TcpTraceroute6 заключается в выполнении трассировки пути между двумя узлами сети. Утилита использует метод `connect()` для установления TCP-соединения к каждому промежуточному хосту. Этот процесс включает отправку ICMP Echo Request сообщений с последующим ожиданием ответа от каждого промежуточного узла. Если ответ не получен, считается, что узел отсутствует или заблокирован.
### 2. Получение IP-адресов
TcpTraceroute6 собирает информацию об IP-адресах всех промежуточных хостов, через которые проходит пакет данных. Это помогает выявить проблемы с маршрутизацией и определить наличие «черных дыр» в сети. Полученные данные могут быть использованы для диагностики проблем с подключением и оптимизации маршрутизации.
### 3. Поддержка IPv6
Важной особенностью утилиты является поддержка работы с адресами IPv6, которые активно используются в современных сетях. Благодаря этому она может эффективно работать с новыми стандартами и предоставлять точную информацию о маршрутах передачи данных.
### 4. Отчетность
По результатам работы утилита предоставляет отчет о пройденном пути, включая временные метки и другую полезную информацию. В отчете отображаются IP-адреса всех промежуточных хостов, время прохождения каждого сегмента пути и статус каждой попытки соединения. Эти данные позволяют быстро оценить состояние сети и выявить потенциальные проблемы.
## Руководство по установке и настройке
### Шаг 1: Загрузка исходного кода
- Перейдите на страницу проекта на GitHub: https://github.com/remlab/ndisc6. 
- Cкачайте архив с исходным кодом утилиты, нажав на кнопку Download ZIP.
### Шаг 2: Распаковка архива
- Распакуйте архив в удобное для вас место. Например, вы можете использовать команду `tar xzvf ndisc6-*.tar.gz`: она распаковывает содержимое архива в текущую директорию.
### Шаг 3: Компиляция утилиты
- Для компиляции утилиты необходимо иметь установленную среду разработки C++. Проверьте, что у вас установлены необходимые инструменты, такие как g++ или clang.
- Перейдите в директорию распакованного архива и запустите команду `make`. Она компилирует исходный код и создает исполняемый файл утилиты. Если все прошло успешно, утилита будет готова к использованию.
## Примеры использования
### Трассировка до адреса IPv6
Чтобы выполнить трассировку до определенного IPv6 адреса, можно использовать следующую команду:
```bash
tcptraceroute6 2001:db8::1
```
### Трассировка с указанием порта
Если нужно проверить конкретный порт, укажите его с помощью параметра `-p`:
```bash
tcptraceroute6 -p 80 2001:db8::1
```
### Установка времени ожидания
Чтобы установить время ожидания для каждого хопа, воспользуйтесь параметром `-w`. Например, установить время ожидания в 2 секунды:
```bash
tcptraceroute6 -w 2 2001:db8::1
```
### Ограничение числа хопов
Если вас интересует только определенное количество хопов, используйте параметр `-m`. Например, ограничить до 10 хопов:
```bash
tcptraceroute6 -m 10 2001:db8::1
```
### Команда с несколькими параметрами
Можно комбинировать параметры. Например, чтобы выполнить трассировку до IPv6 адреса с указанием порта 443, временем ожидания 3 секунды и ограничением по хопам 15:
```bash
tcptraceroute6 -p 443 -w 3 -m 15 2001:db8::1
```
## Отчетность
По завершении трассировки TcpTraceroute6 предоставляет:
- Отчет о времени прохождения каждого сегмента пути, который помогает определить возможные узкие места или проблемы в сети;
- Отчет об IP-адресах всех промежуточных хостов, который позволяет понять структуру сети и выявить возможные точки отказа;
- Отчет о том, были попытки соединения успешными или нет (если соединение не удалось, это может свидетельствовать о проблемах на одном из промежуточных узлов или о наличии блокировок).
## Поддержка и развитие
Проект активно развивается сообществом разработчиков. Вы можете найти актуальную информацию о новых версиях и возможностях утилиты на странице репозитория на GitHub. Если у вас есть предложения или замечания, вы можете оставить их там же.
## Лицензия
В настоящее время распространяется на условиях GNU General Public License, наиболее широко используемой лицензии на программное обеспечение с открытым исходным кодом.
## FAQ
**Какую версию операционной системы поддерживает TcpTraceroute6?** 
> TcpTraceroute6 поддерживает большинство современных версий Unix-подобных операционных систем, включая Linux, BSD и macOS.

**В чем отличие TcpTraceroute6 от традиционного traceroute?** 
> TcpTraceroute6 использует TCP-пакеты для трассировки маршрута, тогда как традиционный traceroute обычно использует UDP или ICMP. Это может помочь обойти ограничения на использование других протоколов.

**Что делать, если я получаю сообщение об ошибке Destination Unreachable?** 
> Это сообщение может указывать на проблему с маршрутизацией, закрытые порты на целевом хосте или конфигурацию брандмауэра. Проверьте эти аспекты.

**Поддерживает ли TcpTraceroute6 IPv4?** 
> Как правило, TcpTraceroute6 предназначен исключительно для IPv6. Для трассировки маршрутов в IPv4 используйте стандартный traceroute или другой соответствующий инструмент.

**Существуют ли альтернативы TcpTraceroute6?** 
> Да, существуют другие инструменты для трассировки маршрутов, включая MTR и обычный traceroute, которые также могут использоваться для диагностики сетевых проблем.
