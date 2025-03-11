# K-ISP-22-Zharkov-W LAB_1
                                                    Введение(08.02.2025)


Перед началом работы, нужно установить Linux Oracle на VirtualBox, с такими характеристиками:

Выделил 2 ядра. Выделил 4096 МБ озу(Иначе процесс установки превратиться в мрак =( ). При установки операционной системы, выбрал английский язык(eng).

Так-же, непосредственно перед основным фронтом работы накатил Guest Additions(Гостевые дополнения) для общего буфера обмена, ну и чтобы окошко растягивать ы

**Гостевые дополнения (Guest Additions)** — это специальные утилиты и драйверы, устанавливаемые в гостевой ОС при использовании виртуализации, например, в нашем случае это VirtualBox. Они предназначены для улучшения взаимодействия между основной и гостевой системой.


                                                  Начало работы(08.02.2025)


Были установлены пакеты **wget** и **curl** с помощью пакетного менеджера **yum**
![image](https://github.com/user-attachments/assets/ec2024c0-5505-472b-abf9-e0c922b3eb31)

    sudo yum install wget

**wget** — это утилита командной строки для загрузки файлов с веб-серверов.

**curl** — это утилита командной строки для передачи данных с или на сервер, поддерживающая множество протоколов, включая HTTP, HTTPS, FTP и другие.

Установка файла репозитория **Docker CE** для **CentOS**
![image](https://github.com/user-attachments/assets/f19baa9f-da6b-438f-9c46-fec2d776b975)

    sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

**-P /etc/yum.repos.d/** — Указывает директорию, в которую будет сохранён загруженный файл.

**https://download.docker.com/linux/centos/docker-ce.repo** — URL файла репозитория **Docker CE** для **CentOS**

Как итог команда была успешно выполнена, и файл **Docker CE** был загружен и сохранён в указанную нами директорию. Он необходим нам для настройки репозитория Docker, что позволит ПМ* **yum** устанавливать пакеты **Docker CE** на нашу систему.

Установка и настройку необходимых пакетов для работы с Docker.
![image](https://github.com/user-attachments/assets/b332da88-bcbd-42eb-9e3c-8a56bd1cace0)

    sudo yum install docker-ce docker-ce-cli containerd.io

**docker-ce** — Основной пакет **Docker Community Edition**.
**docker-ce-cli** — Командная строка Docker для управления **Docker**.
**containerd.io** — Контейнерный рантайм, используемый **Docker**.

Команда была успешно выполнена, и все необходимое для работы с **Docker CE** были установлены на систему. Это позволяет использовать **Docker** для создания и управления контейнерами на системе.

 Этот шаг необходим для того, чтобы Docker мог начать работать после установки.
 ![image](https://github.com/user-attachments/assets/9f25b7d6-d8f0-4279-9495-7fd0c1897e20)

    sudo systemctl enable docker --now

    
Была создана символическая ссылка **/etc/systemd/system/multi-user.target.wants/docker.service**, которая указывает на **/usr/lib/systemd/system/docker.service**.

Теперь **Docker** готов к использованию и будет автоматически запускаться при каждом старте системы.


**Сноска:**

ПМ*- Пакетный менеджер

                                              Продолжение работы(15.02.2025)

Объявление переменной **COMVER**, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose и скачиваем скрипт **docker-compose** последней версии, используя объявленную ранее переменную и помещаем его в каталог **/usr/bin**

![image](https://github.com/user-attachments/assets/3cab9e18-36c6-4c2f-ace4-b7c5fe7a49d3)

    COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
-

    sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

Предоставление прав на выполнение файла **docker-compose.**

![image](https://github.com/user-attachments/assets/812ea156-307a-457a-a0b3-f4fc9a21d096)

    sudo chmod +x /usr/bin/docker-compose

Проверка установленной версии **Docker Compose**.

![image](https://github.com/user-attachments/assets/4e7b62bf-42f4-4b67-984e-b10fbd60a2b7)

    docker-compose --version

После ввода команды **git clone https://github.com/skl256/grafana_stack_for_docker.git** на нашем компьютере создается папка с этим проектом, и в ней будут все файлы, которые есть в этом проекте на GitHub. Это позволит нам работать с этими файлами локально, например, изменять их или просто просматривать.

![image](https://github.com/user-attachments/assets/454eeb87-abac-46ac-a0f2-c50e7d8e7ce6)

    git clone https://github.com/skl256/grafana_stack_for_docker.git

Данной командой мы перешли в папку, которуй созадли ранее 

![image](https://github.com/user-attachments/assets/a783f4a0-0a65-473d-b530-bde9c7ab199b)

    cd grafana_stack_for_docker


Эта команда создает указанную директорию и все необходимые родительские директории.

![image](https://github.com/user-attachments/assets/480c7693-43e8-43c7-9685-35cbdfec8a27)

    sudo mkdir -p /mnt/common_volume/swarm/grafana/config

Создаем три директории: **grafana-config, grafana-data, и prometheus-data внутри /mnt/common_volume/grafana/**.

![image](https://github.com/user-attachments/assets/d5be76ba-7c80-4a9b-9ae2-b9d87889867a)

    sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}

Рекурсивно изменяем владельца и группу для указанных директорий и всех их содержимых файлов и поддиректорий на текущего пользователя и его группу.

![image](https://github.com/user-attachments/assets/ffd08698-c7f3-4bca-b7f7-fefa85a5aed2)

    sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}


Эта команда просто копирует все файлы из папки **config** в другую папку **/mnt/common_volume/swarm/grafana/config/.**

![image](https://github.com/user-attachments/assets/c0c3dbe8-6265-443e-8211-6e5aa951c80e)

    cp config/* /mnt/common_volume/swarm/grafana/config/

 Эта команда переименовывает файл **grafana.yaml** в **docker-compose.yaml**. Это может быть полезно, если вы хотите использовать конфигурацию **Grafana** в качестве конфигурации для **Docker Compose**.

![image](https://github.com/user-attachments/assets/530300dd-b39f-4ddd-b239-11412ea7c73c)

    mv grafana.yaml docker-compose.yaml 

Этой командой мы запускаем все контейнеры, определенные в нашем файле **docker-compose.yaml**, в фоновом режиме с правами суперпользователя. Это удобно для запуска сложных приложений, состоящих из нескольких контейнеров, таких как стек **Grafana**.

![image](https://github.com/user-attachments/assets/1cd765ac-e05c-4d41-8778-4056e01ec89d)

    sudo docker compose up -d

-
                                              Продолжение работы(22.02.2025)

Немного водички

**-d** - Этот флаг означает "запустить в фоновом режиме". Это значит, что контейнеры будут работать независимо, и вы сможете продолжать использовать терминал для других задач.

**pwd** - Команда pwd в терминале показывает, в какой папке вы сейчас находитесь.

***Вода - это хорошо,
Линукс - это вода,
Линукс - это хорошо***



Весь процесс на скриншотах показывает запуск, остановку, перезапуск и удаление стека мониторинга в Docker:

![image](https://github.com/user-attachments/assets/2ddfd13c-a898-44f0-a4e9-72bdd36ce644)
![image](https://github.com/user-attachments/assets/3528ae0a-998d-43d6-8764-8228138fd5fb)

Команда запускает контейнеры в фоновом режиме 

    sudo docker-compose up -d
-
А данная команда в свою очередь, очень важно, останавливает запущенные контейнеры, но не удаляет их.
Контейнеры остаются в состоянии "stopped", и их можно снова запустить с помощью **sudo docker-compose start**

Данные, тома, сеть и конфигурации контейнеров сохраняются.

      sudo docker-compose stop

А с помощью команды 

    sudo docker-compose down

Мы удаляем контейнеры (они больше не появятся в docker ps -a*).

Так-же удаляет созданную сеть (docker network ls**).

Не может удалять тома по умолчанию (но можно добавить --volumes для полного удаления данных).

**Сноска**

*- Выводит список всех контейнеров, включая: Запущенные контейнеры,остановленные контейнеры и контейнеры, завершившие работу (например, с ошибками). Если написать без флажка -a, то выведет только запущенные контейнеры
 
** -  Выводит список всех сетей, созданных в Docker, включая стандартные и пользовательские.

Позанимался бэкапом, ну на всякий, береженого бог бережет(Не заскринил, простите)

    mkdir -p backup

  *


        cp grafana_stack_for_docker/prometeus.yaml backup/


  *

    
        cp grafana_stack_for_docker/docker-compose.yaml backup/


  *


                                            Grafana(О боже, я вмку 3 раза накатывал)

переходим на сайт Графаны  

    localhost:3000

User & Password GRAFANA: 

    admin

В левом меню выбираем вкладку Dashboards и создаем Dashboard
ждем кнопку +Add visualization, а после "Configure a new data source"
![image](https://github.com/user-attachments/assets/5b31ff06-889d-48f3-9cbf-6219e34aa799)
![image](https://github.com/user-attachments/assets/9353ec23-a653-45c2-9b13-5715d259a0aa)


выбираем Prometheus
![image](https://github.com/user-attachments/assets/aa3fed3a-c610-4934-9339-e38c054d2843)

Connection
![image](https://github.com/user-attachments/assets/8fe61438-3ff7-4f23-8deb-e55dbda8b83a)

    http://prometheus:9090

    
Authentication
Basic authentication

User: admin

Password: admin

![image](https://github.com/user-attachments/assets/86ecb527-ea9f-401d-a283-edf21c21e965)

Нажимаем на Save & test и должно показывать зелёную галочку


в меню выбираем вкладку Dashboards и создаем Dashboard
ждем кнопку "Import dashboard"

![image](https://github.com/user-attachments/assets/b1d8c747-66af-4a29-943a-b3a6c107fa5d)

Тут пишем **1860**

![image](https://github.com/user-attachments/assets/d464ea90-b5d8-4d44-973d-028ce150a7a1)

Select Prometheus ждем кнопку "Import"


И о господи оно запустилось 

![image](https://github.com/user-attachments/assets/3bab0bb2-13df-4206-bcf4-29df2212fa4c)

**Слава Богу Lopati🙏❤️СЛАВА LOPATI🙏❤️АНГЕЛА ХРАНИТЕЛЯ LOPATI КАЖДОМУ ИЗ ВАС🙏❤️БОЖЕ ХРАНИ LOPATI🙏❤️СПАСИБО ВАМ НАШИ BRATUXI🙏🏼❤️ХРАНИ LOPATI💯Слава Богу Lopati🙏❤️СЛАВА LOPATI🙏❤️АНГЕЛА ХРАНИТЕЛЯ LOPATI**

