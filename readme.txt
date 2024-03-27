Установка ansible, с root правами.
apt install ansible
Создание структуры каталогов ansible.
mkdir  /etc/ansible/
mkdir  /etc/ansible/web_server_role #Основной каталог ansible в котором будет находиться наш плейбук ngnix.yml
mkdir  cd /etc/ansible/web_server_role/files/ #Каталог для нашего HTML файла test.html 
Создаем файлы в нужном нам каталоге командой touch , пример touch /etc/ansible/web_server_role/files/test.html 
После создания файлов нужно заполнить их пример - nano /etc/ansible/web_server_role/nginx.yml
////////////////////////////////////////////////////////////////////////////////////////////
---
- hosts: all
  tasks:
    - name: Include nginx role
      import_role:
        name: /etc/ansible/web_server_role

    - name: Copy file from local to remote
      copy:
        src: test.html
        dest: /var/www/html/test.html

    - name: Upload nginx configuration file
      template:
        src: /etc/ansible/web_server_role/templates/test.html.j2
        dest: /etc/nginx/sites-available/test.conf
      notify:
        - Restart NGINX
        - Reload NGINX

  handlers:
    - name: Restart NGINX
      service:
        name: nginx
        state: restarted
      
    - name: Reload NGINX
      service:
        name: nginx
        state: reloaded
///////////////////////////////////////////////////////////////////////////////////////////
После этого нужно добавить ключи ssh 
Сгенерируйте новую пару SSH ключей на локальном компьютере с помощью команды: ssh-keygen -t rsa -b 2048
Скопируйте публичный ключ на удаленный хост с помощью команды ssh-copy-id: ssh-copy-id remote_username@remote_host 
Замените remote_username на имя пользователя на удаленном хосте, а remote_host на IP-адрес или доменное имя удаленного хоста.
Подключитесь к удаленному хосту с помощью SSH:  ssh remote_username@remote_host
Можно запускать плейбук ansible-playbook nginx.yml
