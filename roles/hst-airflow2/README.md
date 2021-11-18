# Airflow

Airflow

* presentation: <https://airflow.apache.org/>
* documentation: <https://airflow.apache.org/docs/apache-airflow/stable/index.html>

**WARNING:** default port (8080) is already used on our hosting, changed to 8088

* approximative size: 12MB
* default server port: 8088
* default server version: 1.8.0

## Usage

To known your local adress run command (using SSH)

```bash
echo $LOCALSERVER
```

To configure access to Airflow UI, you need to create a new transparent redirect (reverse proxy) site using the following settings

* type: redirect
* destination URL: http://<LOCAL_ADDRESS>:<AIRFLOW_PORT>
* forwading type: transparent (reverse proxy)