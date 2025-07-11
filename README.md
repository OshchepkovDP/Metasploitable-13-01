# Домашнее задание к занятию "`#«Уязвимости и атаки на информационные системы» - Ощепков Дмитрий`"

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.
---

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
Приведите ответ в свободной форме.

`Ответ`

Найдены уязвимости

`5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7` - версия PostgreSQL ниже версии 9.3, что позволяет выполнить удалённое выполнение кода с последующим удалением следов присутствия.
`5900/tcp open  vnc         VNC (protocol 3.3)` - версия VNC ниже 4.1.1 это приводит к тому, что уязвимость позволяет принудительно установить тип безопасности для сервера secTypeNone, что позволит подключаться к серверу без аутентификации.
`Открыто 22 порта` - большое количество открытых портов повышает уязвимость системы.


1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 1](ссылка на скриншот 1)`


---

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
Как отвечает сервер?
Приведите ответ в свободной форме

Ответ

```Различия режимов сканирования:
SYN-сканирование отправляет полуоткрытые соединения, что мало заметно для систем мониторинга Позволяет точно определить состояние порта.
FIN/Xmas-сканирование использует FIN-пакеты, которые игнорируются открытыми портами. Позволяет обходить некоторые брандмауэры.
UDP-сканирование работает с UDP-портами, отличается меньшей скоростью сканирования. Не требует установки соединения. Присутствуют ложные срабатывания, 
так как отсутствует механизм подтверждения состояния портов. Позволяет находить службы, работающие на нестандартных портах, которые могут быть пропущены при TCP-сканировании.

Ответы сервера
При отправлении пакета с флагом SYN открытый порт отвечает SYN-ACK
При отправлении пакета с флагом FIN открытый порт игнорирует пакет, а закрытый отвечает RST
При Xmas сканировании отправляется пакет с флагами FIN, PSH, URG открытый порт игнорирует пакет, а закрытый отвечает RST
При UDP сканировании отправляется пустой UDP-пакет. Если порт закрыт то приходит ответ, "порт недоступен". Если порт открыт, то ответа нет```

1. ![Файл с записью SYN сканирования](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/synNmap.pcapng)
2. ![Файл с записью FIN сканирования](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/finNmap.pcapng)
3. ![Файл с записью Xmas сканирования](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/XmasNmap.pcapng)
4. ![Файл с записью UDP сканирования](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/udpNmap.pcapng)

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
1. ![SYN-сканирование](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/img/SYN-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.jpg)`
2. ![FIN-сканирование](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/img/FIN-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.jpg)
3. ![Xmas-сканирование](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/img/Xmas-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.jpg)
4. ![UDP-сканирование](https://github.com/OshchepkovDP/Metasploitable-13-01/blob/main/img/UDP-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.jpg)
