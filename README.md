## 🔗 Using-Database-Cluster

- [firstly Create database cluster in digital ocean](https://docs.digitalocean.com/products/databases/mysql/how-to/create/)
- Create new mySql user and database in sever

```
-> mysql -u db_user_name -p -h host -P db_port (or) -> mysql -u doadmin -p<your_password> -h mysql-test-do-user-4915853-0.db.ondigitalocean.com -P 25060 -D defaultdb --ssl-ca=path/to/your-ssl.crt
-> CREATE DATABASE database_name;
-> CREATE USER 'database_user_name'@'%' IDENTIFIED WITH mysql_native_password BY 'YOUR_PASSWORD';
-> GRANT ALL ON db_name.* TO 'database_user_name'@'%';
```
- Add DB cluster in laravel
```
    DB_CONNECTION=mysql
	DB_HOST=127.0.0.1 
	DB_PORT=3306 
	DB_DATABASE=database1 
	DB_USERNAME=root 
	DB_PASSWORD=secret 

	DB_CONNECTION_SECOND=mysql 
	DB_HOST_SECOND=testing-database-do-user-9898878-0.b.db.ondigitalocean.com
	DB_PORT_SECOND=28465 
	DB_DATABASE_SECOND=database_name 
	DB_USERNAME_SECOND=database-user-name
	DB_PASSWORD_SECOND=secret
```
```
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
 ```

 - Schema To specify which connection to use, simply run the connection() method
```
Schema::connection('mysql2')->create('some_table', function($table)
 	{
 	    $table->increments('id'):
 	});

     // query builder
     $users = DB::connection('mysql2')->select(...);

     //Eloquent. Set the $connection variable in your model

 class SomeModel extends Eloquent {
     protected $connection = 'mysql2';
 }


```
#### Benefits of Managed Databases
- https://www.digitalocean.com/community/tech_talks/benefits-of-managed-databases
- https://www.digitalocean.com/community/questions/droplet-mysql-vs-managed-mysql-speed-and-migration

#### REFERENCE
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-scalable-laravel-6-application-using-managed-databases-and-object-storage#step-2-creating-a-new-mysql-user-and-database
- https://codelapan.com/post/how-to-use-multiple-database-connections-in-laravel-8
- https://laravel.com/docs/5.2/database
- https://stackoverflow.com/questions/31847054/how-to-use-multiple-databases-in-laravel
