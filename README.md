#1 : jira-github-jenkins

go to jira -> space -> crate new (asd practical) ->select kanban -> board -> to do -> assign 5 tasks -> create a github repo -> tick the readme on -> jira -> asd practical -> development -> connect -> github-jira -> go to repo -> commit a change -> back to board -> (development:commit) -> check commits ..(commits will be displayed)...(remember add commit msg with  eg.DEVOPS4 / task key)....aws -> login to aws console ->


#2 : git
#3 : jenkins-pipeline
#4 : lambda-dynamodb tbl
#5 : ansible
#6 : docker
#7 : terraform ec2
#8 : lambda-date-time
#9 : airflow
in ubuntu terminal :
sudo apt update
sudo apt install -y python3 python3-venv python3-pip python3-dev build-essential
python3 --version
mkdir -p ~/airflow-practical
cd ~/airflow-practical
python3 -m venv venv
source venv/bin/activate
python -m pip install --upgrade pip
AIRFLOW_VERSION=3.3.2
PYTHON_VERSION="$(python -c 'import sys; print(f"{sys.version_info.major}.{sys.version_info.minor}")')"
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
airflow version
....
export AIRFLOW_HOME=~/airflow
airflow standalone
...if 8080 doesnt work- 
cd ~/airflow-practical -> source venv/bin/activate -> export AIRFLOW_HOME=~/airflow 
(airflow api-server --port 8081)..type this in other ubuntu terminal
now open http://localhost:8081 and login 
use this to get credentials : cat ~/airflow/simple_auth_manager_passwords.json.generated
.....create a DAG file:
nano ~/airflow/dags/date_time_dag.py
{

import pendulum
from airflow.sdk import dag, task


@dag(
    dag_id="date_time_dag",
    schedule="30 9 * * 3",
    start_date=pendulum.datetime(
        2026, 10, 28, tz="Asia/Kolkata"
    ),
    catchup=False,
    tags=["practical"]
)
def date_time_dag():

    @task
    def display_date_time():
        current_time = pendulum.now("Asia/Kolkata")
        print("Current Date:", current_time.date())
        print("Current Time:", current_time.strftime("%H:%M:%S"))

    display_date_time()


date_time_dag()

}
->airflow dags list
...check date_time_dag. appears in the list
next go to airflow page refresh and check for date_time_dag.
run and trigger 




#10 : jenkins-docker
