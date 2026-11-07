---
title: "MySQL SQLAlchemy Conncetor"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-sqlalchemy-conncetor-ce"
---

SQLAlchemy is Python’s SQL toolkit and object\-relational mapper (ORM), enabling developers to interact flexibly with databases in a Pythonic way. It is especially suitable for scenarios requiring object persistence, transaction management, or complex business logic integration with ByteHouse databases through ORM in Python applications. This article demonstrates how to use SQLAlchemy to connect to ByteHouse for data development.

<span id="fac4e3fb"></span>
# Prerequisites

The recommended versions are as follows:


* It is recommended to install [Python 3.12.6](https://www.python.org/downloads/) or higher.

* SQLAlchemy version：2.0.41


<span id="5ca0fea4"></span>
# Caution

Since SQLAlchemy by default sends transaction control commands such as ROLLBACK and COMMIT, which ByteHouse does not support, you need to add the following commands to override related methods and prevent these keywords from being sent. The command examples are as follows:

```Python
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Get MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define a rollback function that performs no action
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original rollback and commit methods of the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---
```


<span id="19850bfa"></span>
# Install SQLAlchemy


1. Install SQLAlchemy and dependencies. For more SQLAlchemy installation instructions, refer to the [SQLAlchemy official documentation](https://www.sqlalchemy.org/).

   ```Python
   pip install SQLAlchemy 
   ```
   

2. Install database\-related drivers for SQLAlchemy.

   * Install pymysql: The MySQL pymysql driver is used as the protocol layer for communication with ByteHouse.

      ```Python
      pip install pymysql 
      ```
      

   * Install cryptography: It is used for encryption and decryption.

      ```Python
      pip install cryptography 
      ```
      


<span id="3650cf34"></span>
# Connect to ByteHouse

Use the following command to connect to ByteHouse.

```Python
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Get MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define an empty rollback function (does nothing)
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original dialect rollback and commit methods
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---

engine = create_engine("mysql+pymysql://{user}:{password}@{bh-host}-public.bytehouse-ce.bytepluses.com:9004", echo=True)
```



|Parameter |Detail |Configuration description |
|---|---|---|
|engine |user |Replace with the actual cluster connection username. You can log in to the ByteHouse console, click **Personal Center** at the top right, then click **Account management** to view and copy the cluster connection account. |
||password |Replace with the cluster connection password. You can log in to the ByteHouse console, click **Personal Center** at the top right, then click **Account management** to view and copy the cluster connection password. |
||bh\-host |The network domain of the ByteHouse instance. Log in to the ByteHouse console, click **Cluster management** at the top, then click the cluster name in the cluster list. View and copy the public/private network information under the **Basic information** tab. |
||echo |Set to true to enable SQL statement log output for easier debugging. |


<span id="1e726e4f"></span>
# Example

<span id="b3acd0d1"></span>
## Use MySQL protocol to connect and query

Connect to ByteHouse via MySQL protocol using SQLAlchemy and execute queries.

```Python
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Obtain the MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define a no-op rollback function (performs no operation)
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original rollback and commit methods of the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---

engine = create_engine("mysql+pymysql://{user}:{password}@{bh-host}-public.bytehouse-ce.bytepluses.com:9004", echo=True)

def simple_select():
    with engine.connect() as conn:
        result = conn.execute(text("select * from user_account"))
        for row in result:
            print("Result:", row[0])
            
if __name__ == '__main__':
    simple_select()
```


**Output result**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d33e3b68886f40b9aa9091462f5705a1~tplv-goo7wpa0wc-image.image" width="1388px" /></div>


<span id="d57f7da5"></span>
## ORM

ORM (Object Relational Mapping) maps object models in object\-oriented programming languages like Python to table structures in relational databases such as MySQL automatically. You can use object\-oriented methods to operate the database without writing native SQL statements.

The following demonstrates writing and querying data in the ByteHouse table `user_account`. This table uses a logically distributed table with the HaMergeTree engine and includes the columns name and fullname.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a3a63b04474863ab025f64fc261f61~tplv-goo7wpa0wc-image.image) </span>

<span id="fec002e8"></span>
### Object persistence write

The data writing command example is as follows. Replace the engine connection details, table name, column names, and attributes with actual information when using.

```Python
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Get the dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define a function that does nothing
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the method on the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---

engine = create_engine("mysql+pymysql://{user}:{password}@{bh-host}-public.bytehouse-ce.bytepluses.com:9004", echo=True)

from typing import Optional
from sqlalchemy import String
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "user_account"
    name: Mapped[str] = mapped_column(String(30), primary_key=True)
    fullname: Mapped[Optional[str]]
    def __repr__(self) -> str:
        return f"User(name={self.name!r}, fullname={self.fullname!r})"

def insert_user():
    from sqlalchemy.orm import Session

    with Session(engine) as session:
        spongebob = User(
            name="spongebob",
            fullname="Spongebob Squarepants",
        )
        sandy = User(
            name="sandy",
            fullname="Sandy Cheeks",
        )
        patrick = User(name="patrick", fullname="Patrick Star")
        session.add_all([spongebob, sandy, patrick])
        session.commit()

if __name__ == '__main__':
    insert_user()
```


**Output result**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e733b18c375845bca6ec0adc4829264c~tplv-goo7wpa0wc-image.image" width="3650px" /></div>


<span id="e9d8c758"></span>
### Query

The data query command example is as follows. Replace the engine connection details, table name, column names, and attributes with actual information when using.

```Python
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section ---
# Get the dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define a function that does nothing
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the method on the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---

engine = create_engine("mysql+pymysql://{user}:{password}@{bh-host}-public.bytehouse-ce.bytepluses.com:9004", echo=True)

from typing import Optional
from sqlalchemy import String
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "user_account"
    name: Mapped[str] = mapped_column(String(30), primary_key=True)
    fullname: Mapped[Optional[str]]
    def __repr__(self) -> str:
        return f"User(name={self.name!r}, fullname={self.fullname!r})"

def select_user():
    from sqlalchemy import select
    from sqlalchemy.orm import Session

    session = Session(engine)

    stmt = select(User).where(User.name.in_(["spongebob"]))

    for user in session.scalars(stmt):
        print(user)
```


**Output results**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12ebbcf61b334cfa83e2e9018a17947e~tplv-goo7wpa0wc-image.image" width="1860px" /></div>


<span id="eee61a21"></span>
# References

For detailed usage of SQlAlchemy, refer to the [official document](https://www.sqlalchemy.org/).
