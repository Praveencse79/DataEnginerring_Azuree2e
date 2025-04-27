# Football Data Engineering

This Python-based project crawls data from Wikipedia using Apache Airflow, cleans it and pushes it Azure Data Lake for processing.
## DataEnginerring_Azuree2e Projects ##

Designed and implemented an end-to-end data pipeline to extract structured football data from Wikipedia using Apache Airflow. Ingested and stored data in Azure Data Lake, orchestrated migration with Azure Data Factory, and performed advanced querying using Azure Synapse Analytics. Delivered actionable insights through interactive visualizations built in Tableau.

ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/topics/dependency-resolution/#dealing-with-dependency-conflicts

pip install --upgrade --force-reinstall fsspec==2024.3.0
pip install --upgrade --force-reinstall dvc

ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
flask-limiter 3.11.0 requires rich<14,>=12, but you have rich 14.0.0 which is incompatible.
limits 4.2 requires packaging<25,>=21, but you have packaging 25.0 which is incompatible.

pip install rich==13.7.1 packaging==24.0
pip install -r requirements.txt

My Container name is "Azure_DataEngineering_e2e"
My Container ID is "9d4fc6830c6ae2ffe85691f5a4905ad5fa1d810768223a9d551f82a0899ac1bf"
localhost:8090:8080 (TCP)

(venv) C:\D_Drive\DataEnginerring_Azuree2e>docker compose up -d
time="2025-04-23T06:59:48+05:30" level=warning msg="C:\\D_Drive\\DataEnginerring_Azuree2e\\docker-compose.yml: the attribute version is obsolete, it will be ignored, please remove it to avoid potential confusion"
[+] Running 3/3
 ✔ Container dataenginerring_azuree2e-postgres-1   Running                                                                                                            0.0s 
 ✔ Container dataenginerring_azuree2e-scheduler-1  Created                                                                                                            0.0s 
 ✘ Container dataenginerring_azuree2e-webserver-1  Error                                                                                                             97.6s 
dependency failed to start: container dataenginerring_azuree2e-webserver-1 is unhealthy

docker compose down -v
docker compose up --build

docker compose ps
The container name (webserver-1)
What it's doing
If it's running, unhealthy, or exited

Apache Airflow
Then webserver is:

The UI layer of Airflow
It lets you log in, view DAGs, trigger workflows, etc.
Runs on port 8080 (or 8090 if you've changed it)

webserver-1 in Docker Compose
In your case, webserver-1 refers to a container that is running a web server service—most likely part of a larger stack defined in your docker-compose.yml. It usually gets its name from the service name in the Compose file.

To check if Apache Airflow is working
1. Check if the webserver is running and healthy :- docker ps
2. Open the Airflow UI in your browser :- http://localhost:8090

To check if a port is already in use (busy) by another process on your system
In cmd:- netstat -aon | findstr :8090

It starts up all the services defined in your docker-compose.yml file in the background (detached mode).
docker compose	Uses Docker Compose (multi-container app manager)
up	Starts (or builds if needed) the containers specified in the YAML file
-d	Runs the containers in detached mode (in the background)

Check the Logs of the Webserver Container
docker logs dataenginerring_azuree2e-webserver-1

Optional Clean-up (if needed)
docker compose down --volumes
docker system prune -af
docker compose up -d

Check webserver container logs
docker compose logs webserver

C:\D_Drive\DataEnginerring_Azuree2e>docker --version
Docker version 28.0.1, build 068a01e

C:\D_Drive\DataEnginerring_Azuree2e>docker-compose --version
Docker Compose version v2.33.1-desktop.1

# Initialize the database if it hasn't been initialized yet #

  airflow db init && \
  airflow users create \
    --username admin \
    --firstname admin \
    --lastname admin \
    --role Admin \
    --email admin@airscholar.com \
    --password admin


# Now you want to verify if everything you set up (DB initialized + admin user created) is actually working. #

Check if Airflow DB is initialized :- airflow db check
Check if Admin User is Created :- airflow users list
Start Airflow Webserver :- airflow webserver

To Login with credentials
Username: admin
Password: admin

Step | Command | What to Expect
DB Initialized | airflow db check | Success message
Admin User Exists | airflow users list | admin listed
Webserver Running | airflow webserver | Visit localhost:8090
Scheduler Running | airflow scheduler | DAGs start executing



docker rmi 0784601dd3b8(Image_ID) --force

Generate a secret key
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"


## Table of Contents

1. [System Architecture](#system-architecture)
2. [Requirements](#requirements)
3. [Getting Started](#getting-started)
4. [Running the Code With Docker](#running-the-code-with-docker)
5. [How It Works](#how-it-works)


## System Architecture
![system_architecture.png](assets%2Fsystem_architecture.png)

## Requirements
- Python 3.9 (minimum)
- Docker
- PostgreSQL
- Apache Airflow 2.6 (minimum)

## Getting Started

1. Clone the repository.
   ```bash
   
   ```

2. Install Python dependencies.
   ```bash
   pip install -r requirements.txt
   ```
   
## Running the Code With Docker

1. Start your services on Docker with
   ```bash
   docker compose up -d
   ``` 
2. Trigger the DAG on the Airflow UI.

## How It Works
1. Fetches data from Wikipedia.
2. Cleans the data.
3. Transforms the data.
4. Pushes the data to Azure Data Lake.
