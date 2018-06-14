# Coisas Úteis

## MySQL
### Criar uma nova base de dados
1. Entrar como root na base de dados `mysql -u root`
2. Utilizar o comando `GRANT ALL PRIVILEGES ON <dbname>.* To '<dbuser>'@'%' IDENTIFIED BY '<dbpwd>';`

## MongoDB
### Criar uma nova base de dados
1. Conectar-se ao MongoDB `mongo`
2. Para criar uma DB, utilizar o comando `use <dbname>`
3. Para criar um user com privilégios, utilizar o comando `db.createUser( { user: "<dbuser>", pwd: "<dbpwd>", roles: [ "readWrite", "dbAdmin" ] } )`
