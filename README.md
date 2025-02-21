# K-ISP-22-Zharkov-W LAB_1
                                                  Начало работы(08.02.2025)


Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Выделить 2+ ядер. Выделать 4096+ МБ озу. При установки операционной системы, нужно будет выбрать английский язык(eng).


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

Предоставление прав на выполнение файла **docker-compose.**

![image](https://github.com/user-attachments/assets/812ea156-307a-457a-a0b3-f4fc9a21d096)

Проверка установленной версии **Docker Compose**.

![image](https://github.com/user-attachments/assets/4e7b62bf-42f4-4b67-984e-b10fbd60a2b7)

После ввода команды **git clone https://github.com/skl256/grafana_stack_for_docker.git** на нашем компьютере создается папка с этим проектом, и в ней будут все файлы, которые есть в этом проекте на GitHub. Это позволит нам работать с этими файлами локально, например, изменять их или просто просматривать.

![image](https://github.com/user-attachments/assets/454eeb87-abac-46ac-a0f2-c50e7d8e7ce6)

Данной командой мы перешли в папку, которуй созадли ранее 

![image](https://github.com/user-attachments/assets/a783f4a0-0a65-473d-b530-bde9c7ab199b)


Эта команда создает указанную директорию и все необходимые родительские директории.

![image](https://github.com/user-attachments/assets/480c7693-43e8-43c7-9685-35cbdfec8a27)



Создаем три директории: **grafana-config, grafana-data, и prometheus-data внутри /mnt/common_volume/grafana/**.

![image](https://github.com/user-attachments/assets/d5be76ba-7c80-4a9b-9ae2-b9d87889867a)

Рекурсивно изменяем владельца и группу для указанных директорий и всех их содержимых файлов и поддиректорий на текущего пользователя и его группу.

![image](https://github.com/user-attachments/assets/ffd08698-c7f3-4bca-b7f7-fefa85a5aed2)


Эта команда просто копирует все файлы из папки **config** в другую папку **/mnt/common_volume/swarm/grafana/config/.**

![image](https://github.com/user-attachments/assets/c0c3dbe8-6265-443e-8211-6e5aa951c80e)

 Эта команда переименовывает файл **grafana.yaml** в **docker-compose.yaml**. Это может быть полезно, если вы хотите использовать конфигурацию **Grafana** в качестве конфигурации для **Docker Compose**.

![image](https://github.com/user-attachments/assets/530300dd-b39f-4ddd-b239-11412ea7c73c)

Этой командой мы запускаем все контейнеры, определенные в нашем файле **docker-compose.yaml**, в фоновом режиме с правами суперпользователя. Это удобно для запуска сложных приложений, состоящих из нескольких контейнеров, таких как стек **Grafana**.

![image](https://github.com/user-attachments/assets/1cd765ac-e05c-4d41-8778-4056e01ec89d)






