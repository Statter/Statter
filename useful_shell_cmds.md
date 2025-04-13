> [!IMPORTANT]
> Данный файл сделан для того, чтобы иметь под рукой список полезных команд консоли `linux`<br/>
> Для некоторых операций нужно добавить в начале команду повышения полномочий (например, `sudo`)

## Базовые утилиты
`arch` = показать текущую архитектуру<br/>
`whoami` = показать текущего пользователя<br/>
`uname -a` = полная информация об операционной системе<br/>
`tar -tvf <tar_archive>` = получить список файлов в архиве tar<br/>
`tar -xvf <tar_archive>` = разъархивировать все файлы в архиве tar<br/>
`curl http://team-nexus.dockerclients.ru:8000/get_request` = сделать HTTP-запрос GET<br/>
`curl -u admin:D5umqPQkaF http://team-nexus.dockerclients.ru:8000/get_request` = сделать HTTP-запрос GET с BASIC аутентификацией<br/>
`curl -v localhost -H 'Host: fin-li.ru'` = симуляция запроса к конкретному домену<br/>
`ls -a /bin | grep '^py'` = выбрать из вывода команды ls все строки, начинающиеся с 'py'<br/>
`ls -ld <directory>` = посмотреть на разрешения для папки<br/>
`ls -l` = посмотреть информация о пользователе и группы, которые являются владельцами, а также правах доступа<br/>
`clear` = очистить окно терминала

## Функционал пользователей и групп linux
`less /etc/passwd` = список всех пользователей linux<br/>
`less /etc/group` = список всех групп linux<br/>
`groupadd <mygroup>` = добавить группу "mygroup"<br/>
`chown <user> <directory>` = поменять владельца папки на указанного<br/>
`chmod 0755 <directory>` = поменять права на папку на указанные<br/>

## Функционал администрирования linux
`sudo -i` = перейти в пользователя root в терминале<br/>
`sudo -s` = перейти в пользователя root в терминале<br/>
`vi /etc/ssh/sshd_config` = посмотреть текущую ssh конфигурацию<br/>
`cat /etc/ssh/sshd_config` = посмотреть текущую ssh конфигурацию<br/>
`nano /etc/ssh/sshd_config` = посмотреть текущую ssh конфигурацию<br/>
`service <service> status` = проверить текущий статус сервиса <service><br/>
`journalctl -u <service>` = зачитать журнал сервиса<br/>
`df -h` = вывод размеров разделов и использованное пространство в человекочитаемом формате<br/>
`lsblk` = вывод подключенных к машине дисков

## ssh/scp
### Базовые команды
`ssh tiny_little_user@91.230.61.199` = открыть новое ssh-подключение к удаленному серверу<br/>
`ssh -i ~/Documents/Finly/finly_rsa.pem.pub tiny_little_user@91.230.61.199` = открыть новое ssh-подключение к удаленному серверу c RSA-ключем<br/>
`ssh -i "D:\VS projects\Finli\finly_rsa.pem" -vT git@github.com` = протестировать подключение по ssh<br/>
`ssh -o ServerAliveInterval=<secs> ...` = установить таймаут бездействия сессии (клиент шлет нулевые пакеты раз 1 в X секунд)<br/>
`who -u` = показать список ssh-сессий<br/>
`sudo kill -HUP 32004` = терминировать ssh-сессию

### Передать локальный файл на удаленный сервер через ssh-подключение
`scp app.py tiny_little_user@91.230.61.199:/opt/feature_sync` <br/>
`scp myfile.txt remoteuser@remoteserver:/remote/folder/` <br/>
`scp -i finly_rsa.pem <file_to_transfer> mikhail@51.250.35.118:/home/mikhail` = передать файл с указанием приватного ключа

### Передать удалённый файл в локальную папку через ssh-подключение
`scp -i "D:\VS projects\PythonSandbox\Projects\Finli\finly_rsa.pem" mikhail@158.160.149.233:<remote_path> <local_path>`

## Gunicorn
https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-gunicorn-and-nginx-on-ubuntu-18-04-ru = настройка gunicorn<br/>
`gunicorn --bind 0.0.0.0:5000 wsgi:app` = запустить приложение

## Docker
`docker container ls` - посмотреть список запущенных контейнеров<br/>
`docker run -d --name phpmyadmin -p 8182:80 -e PMA_HOST=51.250.35.118 phpmyadmin/phpmyadmin` = пример запуска нового контейнера из образа<br/>
`docker container stop phpmyadmin` = пример остановки контейнера<br/>
`docker rm phpmyadmin` = пример удаления контейнера<br/>
`docker exec -it store.web.1 sh` = зайти в терминал контейнера<br/>
`docker inspect phpmyadmin` = вывести текущие настройки контейнера

`docker system prune --all` = удалить все неиспользуемые артефакты:
* all stopped containers
* all networks not used by at least one container
* all dangling images
* all dangling build cache
