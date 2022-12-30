# database-cluster-with-laravel

firstly   Create database cluster in digital ocean 
https://docs.digitalocean.com/products/databases/mysql/how-to/create/

https://docs.digitalocean.com/products/databases/mysql/how-to/connect/#connection-details

Creating mysql user and Database in server

I. mysql -u db_user_name -p -h host -P db_port  (or) mysql -u doadmin -p<your_password> -h mysql-test-do-user-4915853-0.db.ondigitalocean.com -P 25060 -D defaultdb --ssl-ca=path/to/your-ssl.crt


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
3. Add new database cluster setting in laravel 
	
	a. In .env file

		DB_CONNECTION=mysql
		DB_HOST=127.0.0.1 
		DB_PORT=3306 
		DB_DATABASE=database1 
		DB_USERNAME=root 
		DB_PASSWORD=secret 

		DB_CONNECTION_SECOND=mysql 
		DB_HOST_SECOND=testing-database-do-user-9898878-0.b.db.ondigitalocean.com
		DB_PORT_SECOND=28465 
		DB_DATABASE_SECOND=bnfexpress 
		DB_USERNAME_SECOND=bnfexpress-user
		DB_PASSWORD_SECOND=secret

	b. In config/database.php

	 	'mysql' => [
		    'driver'    => env('DB_CONNECTION'),
		    'host'      => env('DB_HOST'),
		    'port'      => env('DB_PORT'),
		    'database'  => env('DB_DATABASE'),
		    'username'  => env('DB_USERNAME'),
		    'password'  => env('DB_PASSWORD'),
		],

		'mysql2' => [
		    'driver'    => env('DB_CONNECTION_SECOND'),
		    'host'      => env('DB_HOST_SECOND'),
		    'port'      => env('DB_PORT_SECOND'),
		    'database'  => env('DB_DATABASE_SECOND'),
		    'username'  => env('DB_USERNAME_SECOND'),
		    'password'  => env('DB_PASSWORD_SECOND'),
		],

	c. Schema
		To specify which connection to use, simply run the connection() method

			Schema::connection('mysql2')->create('some_table', function($table)
			{
			    $table->increments('id'):
			});

	d. Query Builder

		$users = DB::connection('mysql2')->select(...);

	e. Eloquent

		Set the $connection variable in your model

		class SomeModel extends Eloquent {
		    protected $connection = 'mysql2';
		}

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
DB_CONNECTION=mysql

DB_HOST=private-XXXXX.b.db.ondigitalocean.com

DB_PORT=MANAGED_MYSQL_PORT

DB_DATABASE=MANAGED_MYSQL_DB

DB_USERNAME=MANAGED_MYSQL_USER

DB_PASSWORD=MANAGED_MYSQL_PASSWORD
```

