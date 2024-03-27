Установка ansible, с root правами.
apt install ansible
Создание структуры каталогов ansible.
mkdir  /etc/ansible/
mkdir  /etc/ansible/web_server_role #Основной каталог ansible в котором будет находиться наш плейбук ngnix.yml
mkdir  cd /etc/ansible/web_server_role/files/ #Каталог для нашего HTML файла test.html 
Создаем файлы в нужном нам каталоге командой touch , пример touch /etc/ansible/web_server_role/files/test.html 
После создания файлов нужно заполнить их пример - nano /etc/ansible/web_server_role/nginx.yml
После этого нужно добавить ключи ssh 
Сгенерируйте новую пару SSH ключей на локальном компьютере с помощью команды: ssh-keygen -t rsa -b 2048
Скопируйте публичный ключ на удаленный хост с помощью команды ssh-copy-id: ssh-copy-id remote_username@remote_host 
Замените remote_username на имя пользователя на удаленном хосте, а remote_host на IP-адрес или доменное имя удаленного хоста.
Подключитесь к удаленному хосту с помощью SSH:  ssh remote_username@remote_host
Можно запускать плейбук ansible-playbook nginx.yml

