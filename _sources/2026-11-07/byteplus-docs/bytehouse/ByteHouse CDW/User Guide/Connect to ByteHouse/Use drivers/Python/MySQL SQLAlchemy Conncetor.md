---
title: "MySQL SQLAlchemy Conncetor"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-sqlalchemy-conncetor-cdw"
---

SQLAlchemy is a Python SQL toolkit and object\-relational mapper (ORM) that supports project developers to flexibly operate databases in a Pythonic way. It is especially suitable for scenarios requiring object persistence, transaction management, or complex business logic integration with ByteHouse databases through ORM in Python applications. This article demonstrates how to use SQLAlchemy to connect to ByteHouse and develop data.

<span id="f6ff5bf1"></span>
# Prerequisites

The recommended versions are as follows:


* We recommend using [Python 3.12.6](https://www.python.org/downloads/) or higher.

* SQLAlchemy version：2.0.41


<span id="861b000e"></span>
# Restrictions


* ByteHouse JSONB and Bitmap64 data types are not supported.

* If you encounter any other restrictions, contact the ByteHouse team for assistance.


<span id="e598e3bb"></span>
# Caution

Since SQLAlchemy sends transaction control commands like ROLLBACK and COMMIT by default, and ByteHouse does not support these operations, you need to add the following code to override related methods to prevent sending these keywords during execution.

```Python
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql

# --- Monkey Patch Section --- 
# Get MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define an empty rollback function (performs no action)
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original rollback and commit methods of the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---
```


<span id="248dd823"></span>
# Install SQLAlchemy


1. Install SQLAlchemy and dependencies. For more SQLAlchemy installation details, see the [SQLAlchemy official documentation](https://www.sqlalchemy.org/).

   ```Python
   pip install SQLAlchemy 
   ```
   

2. Install SQLAlchemy database\-related drivers.

   * Install pymysql: This driver acts as the protocol layer to communicate with ByteHouse.

      ```Python
      pip install pymysql 
      ```
      

   * Install cryptography: used for encryption and decryption.

      ```Python
      pip install cryptography 
      ```
      


<span id="b3f5cdbd"></span>
# Connect to ByteHouse

Use the following code to connect to ByteHouse.

```Python
from typing import Optional
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql
from sqlalchemy import String
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column

connection_string = "mysql+pymysql://bytehouse:<your_bytehouse_apikey>@<your_bytehouse_host>/<your_database>"

# --- Monkey Patch Section ---
# Get MySQL dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql
# Define an empty rollback function (performs no action)
def no_op_rollback(self, dbapi_connection):
    pass
def do_commit(self, dbapi_connection):
    pass
# Replace the original rollback and commit methods of the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit
# --- End Monkey Patch Section ---
```


**Parameter description**


|Parameter |Details |Configuration Description |
|---|---|---|
|connection_string |<your_bytehouse_apikey\> |Your ByteHouse API key. You can find this in the ByteHouse console under **Tenant management** \> **Connection information**. For how to obtain ByteHouse API key, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
||<your_bytehouse_host\> |Configure the ByteHouse public connection domain, where {TENANT_ID} and {REGION} represent the main account ID of BytePlus and ByteHouse region respectively. You can view this information in the ByteHouse console under \*\*Tenant management \*\*\> \*\*Basic information \*\*\> **Network information**. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for details. |
||<your_database\> |Configure the database name for connecting to ByteHouse. |


<span id="5a38e1a6"></span>
# Example

This example uses the table `user_account` as a test table.

```SQL
CREATE table <your_database>.user_account(
    name string,
    fullname string
) ENGINE=CnchMergeTree 
ORDER BY name
UNIQUE KEY name
```


Use SQLAlchemy to connect to ByteHouse via the MySQL protocol and execute queries.

```Python
from typing import Optional
from sqlalchemy import create_engine, text
from sqlalchemy.dialects.mysql import pymysql as mysql_pymysql
from sqlalchemy import String
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column

# Replace with actual connection information
connection_string = "mysql+pymysql://bytehouse:<your_bytehouse_apikey>@<your_bytehouse_host>/<your_database>"

# --- Monkey Patch Section ---
# Get dialect class
dialect_cls = mysql_pymysql.MySQLDialect_pymysql


# Define an empty rollback function (performs no action)
def no_op_rollback(self, dbapi_connection):
    pass


def do_commit(self, dbapi_connection):
    pass

# Replace the original rollback and commit methods of the dialect class
dialect_cls.do_rollback = no_op_rollback
dialect_cls.do_commit = do_commit

# --- End Monkey Patch Section ---
engine = create_engine(
    connection_string,
)


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
        patrick = User(
            name="patrick",
            fullname="Patrick Star"
        )
        session.add_all([spongebob, sandy, patrick])
        session.commit()


def simple_select():
    with engine.connect() as conn:
        result = conn.execute(text("SELECT 123"))
        for row in result:
            print("Result:", row[0])


def select_user():
    from sqlalchemy import select
    from sqlalchemy.orm import Session

    session = Session(engine)

    stmt = select(User).where(User.name.in_(["spongebob"]))

    for user in session.scalars(stmt):
        print(user)


if __name__ == '__main__':
    simple_select()
    insert_user()
    select_user()
```


<span id="fc5c8ef7"></span>
# References

For SQLAlchemy usage details, refer to the [official documentation](https://www.sqlalchemy.org/).
