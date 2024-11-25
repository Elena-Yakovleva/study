# Виртуальная машина Yandex Cloud

 1. Заходим на сайт https://cloud.yandex.ru/
        2. Выбираем сервис Сompute Cloud
        3. Переходим в раздел виртуальные машины
        4. Создать ВМ
        5. Заполняем «Имя»
        6. В Разделе «Выбор образа/загрузочного диска» выбираем операционную систему Ubuntu версии 20.04
        7. В разделе «диски и файловые хранилища» выбираем тип HDD и уменьшаем размер до 5 Гб (теперь до 10 Гб)
        8. В разделе «вычислительные ресурсы» выбираем "Своя конфигурация" и выбираем: 
* Платформа -Intel Ice Lake, 
* vCPU - 2, 
* Гарантированная доля vCPU - 20%, 
* RAM - 1 Гб, 
* Дополнительно - прерываемая
        9. В разделе «Доступ» убираем галочку "Доступ через OS Login", откроются поля логин и SSH, заполняем логин
        10. Переходим на сайт https://selectel.ru/blog/tutorials/how-to-generate-ssh/
        11. По инструкции генерируем SSH ключ и копируем его в поле SSH-ключ
        12. Нажимаем «создать ВМ»
Если все верно, то стоимость будет около 450 рублей.

# Подготовка проекта для загрузки на сервер

1. Открываем наш проект в IntelliJ IDEA
2. Переходим во вкладку File -> Project Structure
3. Далее в структуре проекта идем в раздел Artifacts
4. Добавляем новый Artifacts, нажимаем «+» -> JAR -> From modules with dependencies
5. В разделе Main Class нажимаем нажимаем на «папку»
6. IDEA будет искать класс с методом main
7. Изменяем директорию файла, удаляем /src/main/resources
8. Нажимаем ОК
9. Далее нажимаем APPLY и затем OK
10.  Переходим в Build -> Build Artifacts
11. Выбираем наш проект.jar -> Build
12. Появится папка out -> artifacts -> наш проект_jar -> наш проект.jar
13. Нажимаем правой кнопкой, кликаем на Copy Path/Reference и копируем абсолютный путь к файлу, он нам понадобится
14. Выбираем Absolute Path

# При подключении:

1. Проверим версию java набирая команду java —version (команда будет не найдена, но будут подсказки по установке java)
2. Набираем команду sudo apt install openjdk-17-jre-headless (либо ту версию, на которой писали проект)
3. На вопрос Do you want to continue? [Y/n] нажимаем enter/return
4. Дожидаемся установки и затем проверим что все прошло удачно, вводим команду java —version и наслаждаемся результатом

❗️ После 4 пункта если Java по-прежнему не установлена, то нужно ввести команду
sudo apt-get update
и повторить 2-3 пункт

# Для передачи файла:

1. Открываем терминал СВОЕГО ПК
2. Вводим команду scp /ТУТ ВАШ ПУТЬ К ФАЙЛУ/НАЗВАНИЕ ФАЙЛА.jar ВАШ_LOGIN@ВАШ_IPv4:
3. В терминале ВМ вводим команду ls (Смотрим что появился наш файл)
4. Вводим команду pwd (смотрим где мы находимся)
5. Открываем страницу https://computingforgeeks.com/how-to-run-java-jar-application-with-systemd-on-linux/
6. Вводим команду sudo groupadd -r appmgr (создает группу пользователей)
7. Вводим команду sudo useradd -r -s /bin/false -g appmgr jvmapps (создаем конкретного пользователя, относящегося к определенной группе пользователей) мы будем запускать программу от имени этого пользователя
8. Вводим команду id jvmapps (проверяем что он создался)
9. Следующий шаг нужно создать программу, вводим команду sudo nano /etc/systemd/system/myapp.service
10. Открывается редактор
11. Копируем и начинаем редактировать
[Unit]
Description=Manage Java service

[Service]
WorkingDirectory=/opt/prod
ExecStart=/bin/java -Xms128m -Xmx256m -jar myapp.jar
User=jvmapps
Type=simple
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target 

12. Редактируем директорию WorkingDirectory=/home/ВАШ_LOGIN, для примера в вебинаре было timur
13. Редактируем название файла, который скачали на ВМ ExecStart=/bin/java -Xms128m -Xmx256m -jar НАЗВАНИЕ ФАЙЛА.jar

Итоговый файл будет таким:
[Unit]
Description=Manage Java service

[Service]
WorkingDirectory=/home/НАЗВАНИЕ ВМ, для примера в вебинаре было timur
ExecStart=/bin/java -Xms128m -Xmx256m -jar НАЗВАНИЕ ФАЙЛА.jar
User=jvmapps
Type=simple
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target

15. Нажимаем для сохранения control + O затем enter/return

Для выхода из редактора nano нажимаем control + X

16. Пользователю которого создали нужно дать ему права для домашней папки (для рабочей папки нашей программы), вводим sudo chown -R jvmapps:appmgr /home/НАЗВАНИЕ ВМ
17. Вводим команду sudo systemctl daemon-reload
18. Вводим команду sudo systemctl start myapp.service
19. Вводим команду systemctl status myapp (проверяем статус работы нашей программы)
20. Чтобы тормознуть программу вводим sudo systemctl stop myapp.service
21. Вводим команду для включения автозапуск программы sudo systemctl enable myapp

