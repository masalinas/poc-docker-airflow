# Description
PoC Apache Airflow installed under docker compose on Ubuntu 20.04 LTS

# Prerequisites
- Install docker CE 20.10+ 
- Install docker-compose 1.29+

# Installation
- Create an airflow working folder:
- Download docker-compose.yaml deployment file:
```shell
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.2.2/docker-compose.yaml'
```
- Create airflow default folders:
```shell
mkdir -p ./dags ./logs ./plugins
```
- Create environment airflow file
```shell
echo -e "AIRFLOW_UID=$(id -u)" > .env
```
- Initialize PostgresSQL and Redis airflow repositories
```shell
docker-compose up airflow-init
```
- Start the airflow services
```shell
docker-compose up
```
- Now we could access airflow UI with default credentials: airflow/airflow from this uri:
```shell
http://localhost:8080
```

![Airflow UI Service](captures/airflow-ui.png "Airflow UI Service")

- We could access airflow CLI from:
First download a wrapper 
```shell
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.2.2/airflow.sh'
chmod +x airflow.sh
```

Go inside airflow container to execute aiarflow CLI commands
```shell
./airflow.sh bash
```

For one-time activation of argcomplete for airflow only, use:
```shell
eval "$(register-python-argcomplete airflow)"
```

Execute any airflow CLI command like this to list all airflow plugins and versions installed
```shell
airflow info
```
