# K-ISP-22-Zharkov-W LAB_1
                                                  Начало работы(08.02.2025)

Были установлены пакеты **wget** и **curl** с помощью пакетного менеджера **yum**
![image](https://github.com/user-attachments/assets/ec2024c0-5505-472b-abf9-e0c922b3eb31)

**wget** — это утилита командной строки для загрузки файлов с веб-серверов.

**curl** — это утилита командной строки для передачи данных с или на сервер, поддерживающая множество протоколов, включая HTTP, HTTPS, FTP и другие.

Установка файла репозитория **Docker CE** для **CentOS**
![image](https://github.com/user-attachments/assets/f19baa9f-da6b-438f-9c46-fec2d776b975)

**-P /etc/yum.repos.d/** — Указывает директорию, в которую будет сохранён загруженный файл.

**https://download.docker.com/linux/centos/docker-ce.repo** — URL файла репозитория **Docker CE** для **CentOS**

Как итог команда была успешно выполнена, и файл **Docker CE** был загружен и сохранён в указанную нами директорию. Он необходим нам для настройки репозитория Docker, что позволит ПМ* **yum** устанавливать пакеты **Docker CE** на нашу систему.

Установка и настройку необходимых пакетов для работы с Docker.
![image](https://github.com/user-attachments/assets/b332da88-bcbd-42eb-9e3c-8a56bd1cace0)

**docker-ce** — Основной пакет **Docker Community Edition**.
**docker-ce-cli** — Командная строка Docker для управления **Docker**.
**containerd.io** — Контейнерный рантайм, используемый **Docker**.

Команда была успешно выполнена, и все необходимое для работы с **Docker CE** были установлены на систему. Это позволяет использовать **Docker** для создания и управления контейнерами на системе.

 Этот шаг необходим для того, чтобы Docker мог начать работать после установки.
 ![image](https://github.com/user-attachments/assets/9f25b7d6-d8f0-4279-9495-7fd0c1897e20)

Была создана символическая ссылка **/etc/systemd/system/multi-user.target.wants/docker.service**, которая указывает на **/usr/lib/systemd/system/docker.service**.

Теперь **Docker** готов к использованию и будет автоматически запускаться при каждом старте системы.


**Сноска:**

ПМ*- Пакетный менеджер
