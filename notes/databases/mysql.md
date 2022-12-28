# MySQL

## Joins

- [Viz for left, right, inner, outer joins](https://joins.spathon.com)
- Self-join- foreign key references a field in the same table (e.g. managerId for employees) [yt vid](https://www.youtube.com/watch?v=7T8b7g7aV1A)

``` mysql
select employee.name as Employee from Employee as employee 
join Employee as manager
on employee.managerId = manager.id
where employee.salary > manager.salary;
```

- in order to use an aggregate function (e.g. `count(*)`) in a select statement, must use group by to specify the column to aggregate on [yt vid](https://www.youtube.com/watch?v=nNrgRVIzeHg)
    - cannot use where (filtering clause) on aggregate function
        - instead use `having` after the groupby statement
- find duplicate email addresses:

``` mysql
select email from Person
group by email
having count(*) > 1;
```

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
