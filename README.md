# Домашнее задание к занятию "`Disaster Recovery.FHRP и Keepalived`" - `Макаров Денис`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

- Дана [схема](https://drive.google.com/file/d/12HCqGj0GEOdQm8HUjHWmOr9zqryAMXFL/view?usp=sharing) для Cisco Packet Tracer, рассматриваемая в лекции.
- На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
- Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
- Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.

### Решение:

"Выполнение задания представлено на скриншотах ниже":

![Снимок42](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/67973403-880f-42ad-8c82-b88c50f04a25)

![Снимок43](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/a56a4228-17fd-41d5-83ac-d5eb9c1e3368)

![Снимок44](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/86ed3555-b336-453a-9956-e690660abc23)
Файл PKT (https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/blob/main/hsrp_advanced_makdi_dz1.pkt).

---


### Задание 2

- Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного [файла](https://github.com/netology-code/sflt-homeworks/blob/main/1/keepalived-simple.conf).
- Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах.
- Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
- Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
- На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html.

### Решение:

#!/bin/bash
   if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then

   
       exit 0
else

       sudo systemctl stop keepalived
       
fi


Файл конфига(https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/blob/main/keepalived.conf)

![Снимок47](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/c65887d5-50e7-4954-b858-e7861b6dd085)


![Снимок45](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/3688cf00-f027-4203-9766-b7c6bb2f39db)

![Снимок48](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/b5148e8b-7daf-4108-be2a-75136bcc6122)


![Снимок46](https://github.com/Makarov-Denis/Disaster-recovery_Keepalived/assets/148921246/599d13dc-ee18-4bae-bb7b-9e7edef8f8c7)


---

