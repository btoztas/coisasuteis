# Coisas Úteis

## MySQL
### Criar uma nova base de dados
1. Entrar como root na base de dados `mysql -u root`.
2. Utilizar o comando `GRANT ALL PRIVILEGES ON <dbname>.* To '<dbuser>'@'%' IDENTIFIED BY '<dbpwd>';`.

## MongoDB
### Criar uma nova base de dados
1. Conectar-se ao MongoDB `mongo`.
2. Para criar uma DB, utilizar o comando `use <dbname>`.
3. Para criar um user com privilégios, utilizar o comando `db.createUser( { user: "<dbuser>", pwd: "<dbpwd>", roles: [ "readWrite", "dbAdmin" ] } )`.

## Apache
### Adicionar um novo web server a apontar para um .wsgi Flask

1. Criar um ficheiro em `/etc/apache2/sites-available/<site>.conf`, com o conteúdo (de seguida um exemplo de Flask):
``
<VirtualHost *:81>
    ServerName wheremi

    WSGIDaemonProcess wheremi python-home=/home/administrator/projects/WhereMi/env python-path=/home/administrator/projects/WhereMi
    WSGIScriptAlias / /home/administrator/projects/wheremi/wheremi.wsgi
    <Directory /home/administrator/projects/wheremi>
        WSGIProcessGroup wheremi
        WSGIApplicationGroup %{GLOBAL}
        Require all granted
    </Directory>
</VirtualHost>
``

2. Criar um .wsgi com o conteúdo (de seguida um exemplo de Flask):
``
import sys
sys.path.insert(0, '/path/to/the/application')

from wheremi import app as application
``
3. Verificar de em `vim /etc/apache2/ports.conf` a porta escolhida para o webserver está marcada como Listen, se não adicionar `Listen <port>` ao ficheiro.

4. Para ativar o site utilizar o comando `a2ensite <sitename>` e fazer reload ao apache com `systemctl reload apache2`.
