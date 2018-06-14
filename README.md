# Coisas Úteis

## MySQL
### Criar uma nova base de dados e respetivo utilizador
1. Entrar como root na base de dados `mysql -u root`.
2. Criar uma base de dados com `CREATE DATABASE <dbname>;`.
3. Verificar a criação da bd com`SHOW DATABASES;`.
3. Criar um user com `CREATE USER '<dbuser>'@'%' IDENTIFIED BY '<dbpwd>';`.
4. Verificar a criação do user `SELECT * FROM mysql.user;`.
5. Dar privilégios ao user na db com `GRANT ALL PRIVILEGES ON <dbname> . * TO '<dbuser>'@'%';`.
6. Atualizar políticas com `FLUSH PRIVILEGES;`.

## MongoDB
### Criar uma nova base de dados
1. Conectar-se ao MongoDB `mongo`.
2. Para criar uma DB, utilizar o comando `use <dbname>`.
3. Para criar um user com privilégios, utilizar o comando `db.createUser( { user: "<dbuser>", pwd: "<dbpwd>", roles: [ "readWrite", "dbAdmin" ] } )`.

## Apache
### Adicionar um novo web server a apontar para um .wsgi Flask

1. Criar um ficheiro em `/etc/apache2/sites-available/<site>.conf`, com o conteúdo (de seguida um exemplo de Flask):
```
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
```

2. Criar um .wsgi com o conteúdo (de seguida um exemplo de Flask):
```
activate_this = '/home/administrator/projects/stacker/env/bin/activate_this.py'
execfile(activate_this, dict(__file__=activate_this))

from stacker_app import app as application
```
3. Verificar de em `vim /etc/apache2/ports.conf` a porta escolhida para o webserver está marcada como Listen, se não adicionar `Listen <port>` ao ficheiro.

4. Para ativar o site utilizar o comando `a2ensite <sitename>` e fazer reload ao apache com `systemctl reload apache2`.
