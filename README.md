# Cloud-function-to-trigger-Composer-DAG
Cloud function triggered when a CSV file placed into the triggered landing storage bucket path and invoke the Composer DAG to load CSV data into BigQuery table 

# Steps to load CSV to BQ table

### Create one landing buckets 
i.e. trigger bucket for function i.e. third-campus-303308-cf-landing

### Composer-to-load-CSV-to-BQ
Refer the github link https://github.com/trushasahu/Composer-to-load-CSV-to-BQ 

Note: By default, the API authentication feature is disabled in Airflow 1.10.11 and later versions. The Airflow web server denies all requests that you make. You use requests to trigger DAGs, so enable this feature. Refer the link https://cloud.google.com/composer/docs/how-to/using/triggering-with-gcf#console to override the airflow configuration and enable the API authentication feature. So cloud fnction can invoke the DAG.

### Create cloud function using content in function folder
1- Create function with name 'func-trigger-a-composer-dag' with below details

  -Function name :  func-trigger-a-composer-dag
  
  -Region : europe-west2     --the region should be same for storage, function and dataflow to avoid the failure

  -Trigger type : Cloud storage
  
  -Event type : Finalize/Create
  
  -bucket : third-campus-303308-cf-landing    --i.e. triggered landing bucket
  
  -Source : edit the main.py and requirements.txt 
      i.e. copy the code from CF_to_trigger_Composer_dag.py into the main.py 
      and  copy the code from requirements.txt to requirements.txt
      
  -Runtime : Python 3.7
  
  -Entry point : trigger_dag   i.e. function name of the main.py code
  
### Place the csv file into the  third-campus-303308-cf-landing  bucket to tigger the function and Composer DAG 'gcs_to_bigquery_operator' to load data into bigquery table.
