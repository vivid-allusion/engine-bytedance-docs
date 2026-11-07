---
title: "Apache Airflow"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-connect-airflow-to-bytehouse-and-schedule-queriesdata-loading"
---

Apache Airflow is an open\-source platform for developing, scheduling, and monitoring batch workflows.

<span id="ca0b4160"></span>
## Prerequisites


* Install `pip` in your virtual/local environment.

* Install `ByteHouse CLI` in your virtual/local environment and log in with your own ByteHouse account. For Mac OS, you can install it directly via homebrew. For other installation methods, refer to [ByteHouse CLI](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client).


```plaintext
brew install bytehouse-cli
```


<span id="9e27d8c1"></span>
## Install Airflow

First, install Apache Airflow in your local or virtual environment. In this tutorial, we use `pip` to install. For other installation methods, please view the [Apache Airflow official documentation](https://airflow.apache.org/docs/apache-airflow/stable/installation/installing-from-pypi.html) for more details.

```shell
# To use Airflow, you need to specify a directory; default directory is ~/airflow，
# If you prefer, you can choose another location 
# (optional)
export AIRFLOW_HOME=~/airflow

# run the following 
AIRFLOW_VERSION=2.7.0
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"

CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If installation using <code>pip</code> fails, try to install using the <code>pip3 install</code> command based on your Python version.</div>


After installation is complete, run the command `airflow info` to obtain more information about Airflow.

<span id="0c6e6132"></span>
## Initialize Airflow

Initialize the Airflow Web server by running the following commands:

```shell
# initialise the database
airflow db init

airflow users create \
    --username admin \
    --firstname admin \
    --lastname admin \
    --role Admin \
    --email admin 
# start the web server, default port is 8080
# or modify airflow.cfg set web_server_port 
airflow webserver --port 8080
```


After setting up the Web server, you can access http://localhost:8080/ and log in to the Airflow console using the username and password you set up before.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c66bfeb02fd243fccba955f96b1b29f.jpg) </span>

In a new terminal, set up the Airflow scheduler with the following commands, and then refresh http://localhost:8080/.

```plain
# start the scheduler
# open a new terminal or else run web server with ``-D`` option to run it as a daemon
airflow scheduler
# visit localhost:8080 in the browser and use the admin account you just
# created to login. Enable the example_bash_operator dag in the home page
```


<span id="6041dff1"></span>
## Create DAG Jobs

Create a folder named dags under the airflow pat`dags under the airflow` path and then create `test_bytehouse.py` to launch new DAG jobs.

```shell
~/airflow
mkdir dags
cd dags
nano test_bytehouse.py
```


In `test_bytehouse.py`, add the following code, which can connect to the ByteHouse CLI and use BashOperator to run tasks, executing queries or loading data into ByteHouse.

```python
from datetime import timedelta
import pendulum
from airflow import DAG
from airflow.operators.bash import BashOperator
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email': ['airflow@example.com'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=1),
}
# Create the DAG instance
with DAG(
    'test_bytehouse',
    default_args=default_args,
    description='A simple tutorial DAG',
    schedule=timedelta(days=1),  
    start_date=pendulum.today('UTC').add(days=-1),
    tags=['example'],
) as dag:
    # Define the BashOperators
    tCreateDatabase = BashOperator(
        task_id='ch_database',
        depends_on_past=False,
        bash_command='bytehouse-cli --host {HOST} --port {PORT} --secure --token {API_KEY} -q "CREATE DATABASE airflow_demo"'
    )
    
    tCreateTable = BashOperator(
        task_id='ch_table',
        depends_on_past=False,
        bash_command='bytehouse-cli --host {HOST} --port {PORT} --secure --token {API_KEY} -q "CREATE TABLE airflow_demo.demo_tb(id UInt64) ENGINE=CnchMergeTree() ORDER BY id"'
    )
    
    tImport = BashOperator(
        task_id='ch_import',
        depends_on_past=False,
        bash_command='bytehouse-cli --host {HOST} --port {PORT} --secure --token {API_KEY} -q "INSERT INTO airflow_demo.demo_tb values (1)"',
    )
    
    tSelect = BashOperator(
        task_id='ch_select',
        depends_on_past=False,
        bash_command='bytehouse-cli --host {HOST} --port {PORT} --secure --token {API_KEY} -q "SELECT * FROM airflow_demo.user"',
    )
    tCreateDatabase >> tCreateTable >> tImport >> tSelect
```


Run `python test_bytehouse.py` in the current file path to create a DAG in Airflow.

Refresh the web page in your browser, and you will see the newly created DAG named `test_bytehouse` displayed in the DAG list.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_364e3d88a4733cf38331058f63e9ae3f.png) </span>

Run the following Airflow command in the terminal to view the list of DAGs and the test subtasks in the `test_Bytehouse` DAG. You can test query execution and data import tasks separately.

```shell
#prints the list of tasks in the "test_bytehouse" DAG
airflow tasks list test_bytehouse
#output
ch_database
ch_import
ch_select
ch_table

#prints the hierarchy of tasks in the "test_bytehouse" DAG
airflow tasks list test_bytehouse --tree
#output

    
        
            
```


After the DAG runs successfully, you will see a success indicator in the DAG.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98fb42341ab748bbb62d872d6f65d5a1~tplv-goo7wpa0wc-image.image) </span>

Check the query history page and database modules in your ByteHouse account, and you will see the data has been successfully queried/loaded.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f59bdb7295427986179a97832fb9fc~tplv-goo7wpa0wc-image.image) </span>
