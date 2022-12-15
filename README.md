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
[2022-12-13 17:16:40] production.DEBUG: Guest -  Requested https://bnftopup.com/topup/payment_status/e_wallet/h1XbUkvgngF-Eyk-0lOqZw==(POST) ::: {"ip":"162.158.163.23","device":" Unknown","user_agent":null,"platform":" Unknown","data":"{\"version\":\"6.2\",\"request_timestamp\":\"2022-12-13 17:15:17\",\"merchant_id\":\"104104000000038\",\"order_id\":\"00000000004379131222\",\"invoice_no\":\"63985794a84b34379\",\"currency\":\"104\",\"amount\":\"000003090000\",\"transaction_ref\":\"212804756\",\"approval_code\":\"198769\",\"eci\":\"xx\",\"transaction_datetime\":\"2022-12-13 17:16:40\",\"payment_channel\":\"001\",\"payment_status\":\"000\",\"channel_response_code\":\"00\",\"channel_response_desc\":\"Approved\",\"masked_pan\":null,\"stored_card_unique_id\":null,\"backend_invoice\":\"167090642\",\"paid_channel\":null,\"paid_agent\":null,\"user_defined_1\":\"h1XbUkvgngF-Eyk-0lOqZw==\",\"user_defined_2\":\"topup\",\"user_defined_3\":null,\"user_defined_4\":null,\"user_defined_5\":null,\"browser_info\":null,\"hash_value\":\"238B2A106C76DA2EABAAA09F8C4622C601C3204C\"}"} 
```

