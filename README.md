# database-cluster-with-laravel

firstly   Create database cluster in digital ocean 
https://docs.digitalocean.com/products/databases/mysql/how-to/create/

https://docs.digitalocean.com/products/databases/mysql/how-to/connect/#connection-details

Creating mysql user and Database in server

I. mysql -u db_name -p -h host -P db_port  (or) mysql -u doadmin -p<your_password> -h mysql-test-do-user-4915853-0.db.ondigitalocean.com -P 25060 -D defaultdb --ssl-ca=path/to/your-ssl.crt


II. create database;

III.CREATE USER 'name-user'@'%' IDENTIFIED WITH mysql_native_password BY 'your_password';

IV. GRANT ALL ON db_name.* TO 'name-user'@'%';


and then change .env 

...

DB_CONNECTION=mysql

DB_HOST=private-XXXXX.b.db.ondigitalocean.com

DB_PORT=MANAGED_MYSQL_PORT

DB_DATABASE=MANAGED_MYSQL_DB

DB_USERNAME=MANAGED_MYSQL_USER

DB_PASSWORD=MANAGED_MYSQL_PASSWORD

...
