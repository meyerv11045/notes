# MySQL

## Python Access
1. Connect to the MySQL Database, you get a MySQLConnection object.
	a. To connect to the database, read the database configuration parameters from config.ini using configparser and pass the resulting dictionary to the constructor of the MySQLConnection Object
2. Instantiate a  MySQLCursor object from the the MySQLConnection object.
3. Use the cursor to execute a query by calling its  execute() method.
4. Use fetchone() ,  fetchmany() or  fetchall() method to fetch data from the result set.
5. Close the cursor as well as the database connection by calling the  close() method of the corresponding object

```python
from mysql.connector import MySQLConnection, Error

dbconfig = {
    'host' = 'localhost',
    'database' = 'Books',
    'user' = 'root',
    'password' = 'password'    
}

conn = None
try:
    conn = MySQLConnection(**dbconfig)   
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM books LIMIT 5')

    for row in iter_row(cursor):
        print(row)

except Error as e:
    print(e)

finally:
    cursor.close()
    conn.close()

```

Generator that chunks the database calls into a series of fetchmany() calls
```python
def iter_row(cursor,size=10):
	while True:
		rows = cursor.fetchmany(size)
		if not rows:
			break
		for row in rows:
			yield row
```
