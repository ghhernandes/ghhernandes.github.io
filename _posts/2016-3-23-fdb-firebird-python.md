---
layout: post
title: FDB - Firebird with Python
---
This documentation give a brief of firebird database on python.
FDB is written as pure-Python module on top of Firebird client library (fbclient) using [ctypes](https://docs.python.org/2/library/ctypes.html).

*Make sure you have Firebird client properly installed before.*

## Installation from PIP
Run pip and wait:
``
$ pip install fdb
``


```
$ pip install fdb
```

## Installation from source

Download the source, uncompress it, then run the install command:

```
$ curl -O http://pypi.python.org/packages/source/f/fdb/fdb-0.9.1.tar.gz
$ tar -xzvf fdb-0.9.1.tar.gz
$ cd fdb-0.9.1
$ python setup.py install
```

## Connecting to a Database

**1. Example**

Basic connection:

```
import fdb

con = fdb.connect(host='server', database='/temp/test.fdb',
                  user='sysdba', password='masterkey')
```

**2. Example**

Suppose we want to connect to the database in SQL Dialect 1 and specifying UTF-8 as the character set of the connection:
```
import fdb

con = fdb.connect(host='server', database='/temp/test.fdb',
                  user='sysdba', password='masterkey',
                  sql_dialect=1, charset='UTF8')
```

## Executing SQL Statements

Suppose we have a table defined and populated by the following SQL code:

```
create table users
(
  user_name          varchar(20),
  user_password      varchar(20)
);

insert into users (user_name, user_password) values ('admin', 'admin');
insert into users (user_name, user_password) values ('jhon',    '123');
insert into users (user_name, user_password) values ('marie',   '321');
```

**Example**

```
import fdb

con = fdb.connect(host='server', database='/temp/test.fdb',
                  user='sysdba', password='masterkey')

# Create a Cursor object that operates in the context of Connection con:
cur = con.cursor()

# Execute the SELECT statement:
cur.execute("select * from users order by user_name")

# Retrieve all rows as a sequence and print that sequence:
print cur.fetchall()
```

Sample output:

```
[('admin', 'admin'), ('jhon', '123'), ('marie', '321')]
```

For more informations, visit [FDB references](http://pythonhosted.org/fdb/reference.html).
