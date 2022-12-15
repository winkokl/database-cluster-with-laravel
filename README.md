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


Digital Ocean not allowed without primary key 

if you found like this err "Unable to create or change a table without a primary key, when the system variable 'sql_require_primary_key' is set."

Steps To Reproduce:

Ensure sql_require_primary_key is enabled on the MySQL server

Create a migration that creates a new table with a string as the primary key (we used $table->string('string')->primary();) and does not have a default $table->id(); column

Run the migration

AND can solve with adding (SET SESSION sql_require_primary_key=0) at the beginning of export sql 


Benefits of Managed Databases

https://www.digitalocean.com/community/tech_talks/benefits-of-managed-databases

https://www.digitalocean.com/community/questions/droplet-mysql-vs-managed-mysql-speed-and-migration

REFERENCE

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-scalable-laravel-6-application-using-managed-databases-and-object-storage#step-2-creating-a-new-mysql-user-and-database

https://codelapan.com/post/how-to-use-multiple-database-connections-in-laravel-8

https://laravel.com/docs/5.2/database

https://stackoverflow.com/questions/31847054/how-to-use-multiple-databases-in-laravel


```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

