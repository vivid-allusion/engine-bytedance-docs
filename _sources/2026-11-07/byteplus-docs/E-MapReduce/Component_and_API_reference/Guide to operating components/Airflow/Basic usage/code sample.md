---
title: "code sample"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/code_sample"
---

This article introduces the usage of Spark Operator, Hive Operator, and Presto (Trino) Operator through examples, helping you become familiar with the collaborative workflow between Airflow and other big data components.

<span id="_1-前提条件"></span>
## Prerequisites

All examples are based on a Hadoop cluster with Airflow and Presto services added. For details on cluster creation, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-spark-operator-使用示例"></span>
## Spark Operator usage example

Note: The SparkPi example is run using spark\-submit, then a request to create a new table is submitted via spark\-sql, data is inserted and viewed, and finally a UDF is executed.

This scenario covers the main cases involved in Spark's daily operations. Airflow provides two operators for Spark: SparkSubmitOperator and SparkSQLOperator.

```python
from airflow.models import DAG
from airflow.providers.apache.spark.operators.spark_submit import SparkSubmitOperator
from airflow.providers.apache.spark.operators.spark_sql import SparkSqlOperator
from airflow.utils.dates import days_ago

args = {
    'owner': 'hive',
}
with DAG(
    dag_id='emr_spark_test',
    default_args=args,
    schedule_interval='30 * * * *',
    start_date=days_ago(2),
    tags=['example'],
) as dag:
    
    spark_submit_case = SparkSubmitOperator(
        task_id='spark_submit',
        dag=dag,
        application= 'path_to_example_jar',
        java_class='org.apache.spark.examples.SparkPi',
        name='airflow-spark-submit'
        # executor_cores= 1,
        # executor_memory='1g',
        # driver_memory='1g',
    )
    
    # [START emr-demo]
    create_table_job = SparkSqlOperator(
        task_id='run_first',
        sql='''
        create database if not exists airflow;
        use airflow;
        drop table if exists sparksql_operator_test;
        create table sparksql_operator_test(name string);
        insert into sparksql_operator_test values('test');
        ''',
        name='airflow-spark-sql-create-table'
        # conn_id='spark_sql_default',
        # keytab=Node,
        # total_executor_cores=None,
        # executor_cores=None,
        # executor_memory=None,
        # conf='spark.sql.shuffle.partitions=100',
        # principal=None,
        # master='yarn',
        # num_executors=None,
        # verbose=True,
        # yarn_queue='default'
    )
    
    select_job = SparkSqlOperator(
        task_id='run_second',
        sql='''
        use airflow;
        select name from sparksql_operator_test;
        ''',
        master='yarn',
        name='airflow-spark-sql-select'
    )
    
    udf_case = SparkSqlOperator(
        task_id='run_second',
        sql='''
        use airflow;
        select udf_name(name) from sparksql_operator_test;
        ''',
        master='yarn',
        name='airflow-spark-sql-select'
    )
    
    spark_submit_case >> create_table_job >> select_job >> udf_case
    # [END how_to_operator_spark_sql]
```


<span id="_3-hive-operator-使用示例"></span>
## Hive Operator usage example

Note: A table is created and data is inserted using HiveSQL, and finally a UDF is executed.

The HiveOperator provided by Airflow is used to execute HiveSQL, which can cover the above scenario.

```python
from airflow import DAG
from airflow.operators.hive_operator import HiveOperator
from datetime import datetime, timedelta
from airflow.models import Variable
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2019, 6, 1),
    'email': ['airflow@example.com'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=1),
    'end_date': datetime(9999, 1, 1),}
    
dag = DAG(
    'hive_test_dag', 
    default_args=default_args, 
    schedule_interval='30 10 * * *', 
    catchup=False)
    
hive_drop_case = HiveOperator(
    task_id='hive_test_task1',
    hive_cli_conn_id='hiveserver2',
    schema='default',
    hql='DROP TABLE IF EXISTS example;',
    dag=dag)
        
hive_create_case = HiveOperator(
    task_id='hive_test_task2',
    hive_cli_conn_id='hiveserver2',
    schema='default',
    hql='''
CREATE TABLE example (cid INT, cnm STRING, cam DECIMAL(18,2), ctm TIMESTAMP) 
PARTITIONED BY (dt string) STORED AS PARQUET;
    ''',
    dag=dag)
    
hive_insert_case = HiveOperator(
    task_id='hive_test_task3',
    hive_cli_conn_id='hiveserver2',
    schema='default',
    hql='''
INSERT INTO example PARTITION (dt) 
SELECT
  LPAD(ROW_NUMBER() OVER (ORDER BY dummy),10,'0') AS cid,
  CONCAT('Name', LPAD(ROW_NUMBER() OVER (ORDER BY dummy),5,'0')) AS cnm,
  ROUND(RAND() * RAND() * 10000,2) AS cam,
  CURRENT_TIMESTAMP() AS ctm,
  DATE_FORMAT(DATE_ADD(CURRENT_DATE(), -CAST(FLOOR(RAND()*3) AS INT)), 'yyyyMMdd') AS dt
FROM (
  SELECT EXPLODE(SPLIT(REPEAT('x', 29), 'x')) AS dummy
) tmp;
    ''',
    dag=dag)
    
hive_select_case = HiveOperator(
    task_id='hive_test_task4',
    hive_cli_conn_id='hiveserver2',
    schema='default',
    hql='SELECT * FROM example ORDER BY cid;',
    dag=dag)
    
hive_drop_case >> hive_create_case >> hive_insert_case >> hive_select_case
```


<span id="_4-presto-operator-使用示例"></span>
## Presto Operator usage example

Note: A table is created using Presto, data is inserted, and then read out.

The functionality provided by Airflow's Presto Provider is relatively limited, offering only the basic presto_hook. You need to write Python methods based on this hook to complete tasks; workflows cannot be simply created and orchestrated using Operator objects. Airflow provides a generic PythonOperator, which allows you to schedule any Python method.

```python
from airflow import DAG
from airflow.hooks.presto_hook import PrestoHook
from airflow.operators.python_operator import PythonOperator
from datetime import timedelta

default_args = {
    'owner': 'airflow',
    'depends_on_past':  False,
    'start_date':airflow.utils.dates.days_ago(0),
    'email': ['airflow@example.com'],
    'email_on_failure': True,
    'email_on_retry': False,
    'retries':3,
    'retry_delay':timedelta(minutes=15),}

dag = DAG(
    'Presto-demo',
    default_args=default_args,
    description='Presto demo',
    schedule_interval=timedelta(minutes=30))
    
# Use the connector_id for presto; this Conn has already been initialized for you
ph = PrestoHook(
    presto_conn_id='presto',
    catalog='hive',
    schema='default',
    port=8080)

def presto_drop_table(**context):
    sql = """DROP TABLE IF EXISTS tb_airflow_demo"""
    data = ph.get_records(sql)
    return True

def presto_create_table(**context):
   sql = '''
   CREATE TABLE IF NOT EXISTS tb_airflow_demo(id int, name varchar)
   '''
   data = ph.get_records(sql)
   return True
   
def presto_insert_data(**context):
    sql = '''
    INSERT INTO tb_airflow_demo SELECT 1, 'name1'
    '''
    data = ph.get_records(sql)
    return True


def presto_select_data(**context):
    sql = '''
    SELECT * FROM tb_airflow_demo LIMIT 20
    '''
    data = ph.get_records(sql)
    return True

# It is best not to execute drop table; without configuration in presto, this permission is generally unavailable and the task will fail
#presto_drop_table_task = PythonOperator(task_id='presto_drop_table',provide_context=True,python_callable=presto_drop_table,dag=dag)

presto_create_table_task = 
    PythonOperator(
        task_id='presto_create_table',
        provide_context=True,
        python_callable=presto_create_table,
        dag=dag)
        
presto_insert_data_task = 
    PythonOperator(
        task_id='presto_insert_data',
        provide_context=True,
        python_callable=presto_insert_data,
        dag=dag)
        
presto_select_data_task = 
    PythonOperator(
        task_id='presto_select_data',
        provide_context=True,
        python_callable=presto_select_data,
        dag=dag)
        
presto_create_table_task >> presto_insert_data_task >> presto_select_data_task

if __name__ == "__main__":
    dag.cli()
```


<span id="_4-1-presto-中的-drop-alter-权限"></span>
### Drop/alter permissions in Presto

This DAG example comments out the `drop_table` section. To have drop/alter table permissions when executing in Presto, add configuration items for the Presto component in the EMR console as shown in the illustration. The configuration items are as follows.

```plain
hive.allow-drop-table=true
hive.allow-rename-table=true
hive.allow-add-column=true
hive.allow-drop-column=true
hive.allow-rename-column=true
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b951744d00da7cd91c61be7c6497803.png) </span>


* After completing the configuration and deployment, please restart the component.
