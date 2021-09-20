# Apache-Sqoop-
Apache Sqoop all imports and exports commands\

# Sqoop import :- transfer data from RDBMS to HDFS.Sqoop is a tool designed to transfer data between hadoop and relational databases.
# Records are stored in Text file format,Sequence File format,Auro & Parquet file format.

# Sqoop-eval :- To run quueries on databases.

# To get all the commands
  sqoop help
  
# To know about the Version
  sqoop version

# Commands for Imports 

# .List of databases :- It will show all the databases.
 sqoop-list-databases \
 --connect "jdbc:mysql://quickstart.cloudera:3306" \
 --username root \
 --password cloudera \


# list of tables :- it will show all the list of tables.

sqoop-list-tables \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \

# display the table connect
sqoop-eval \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --e "select * from retail_db.orders limit 10"
 
 # Import data from MySQL to Sqoop
sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --target-dir /user 
 
 # By changing mapper we can import
 sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --m 1\
 --warehouse-dir /user/xyz/folder1
 
 # To store some output and error
 sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --warehouse-dir /queryresult 1>query.out 2>query.err
 
 
 # Compress while importing
  sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --compress \
 --warehouse-dir /user/xyz/folder1
 
 
 # Hadoop Compression codec
   sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --compression-codec BZip2Codec \
 --warehouse-dir /user/xyz/folder1
 
 
 # Import the data with selected columns
   sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table customers \
 --columns customer_id,customer_fname \
 --warehouse-dir /user/xyz/folder1
 
 # Import the data with Where clause 
   sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --columns customer_id,customer_fname \
 --where "order_status in ('complete','closed')" \
 --warehouse-dir /user/xyz/folder1
 
 # Tell Computer about the boundary query
  sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --boundary-query "SELECT 1,675678" \
 --warehouse-dir /user/xyz/folder1
 
 # Split By :- If their is no primary key then we can use split-by to indicate the column based on which mapper should divide the work.
 
  sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --split-by order_id \
 --warehouse-dir /user/xyz/folder1


# Delimiters in Sqoop
  sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --fields-terminated-by '|' \
 --lines-terminated-by ';' \
 --warehouse-dir /user/xyz/folder1
 
 
# Sqoop Verbose :- Generate logs and debugging information 
 sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --verbose \
 --warehouse-dir /user/xyz/folder1
 
 
 
 # Sqoop Append :- append is used to add into share directory
  sqoop-import \
 --connect "jdbc:mysql://quickstart.cloudera:3306/retail_db" \
 --username root \
 --password cloudera \
 --table orders \
 --columns customer_id,customer_fname \
 --where "order_status in ('complete','closed')" \
 --warehouse-dir /user/xyz/folder1
 --append

 

