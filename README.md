# docker_varios

PASOS

#!/bin/bash

useradd pgadmin
usermod -u 5050 pgadmin
usermod -g 5050 pgadmin

useradd postgres
usermod -u 5051 postgres
usermod -g 5051 postgres

useradd sonarqube
usermod -u 5052 sonarqube
usermod -g 5052 sonarqube


mkdir db-data
mkdir sonarqube_data
mkdir sonarqube_extensions
mkdir sonarqube_logs
mkdir pgadmin-data
mkdir sonarqube_extensions/plugins

cd sonarqube_extensions/plugins
wget https://binaries.sonarsource.com/Distribution/sonar-auth-bitbucket-plugin/sonar-auth-bitbucket-plugin-1.1.0.381.jar

chown -R pgadmin:pgadmin pgadmin-data

chown -R postgres:postgres db-data

chown -R sonarqube:sonarqube sonarqube_*


Correr docker compose
docker-compose up -d
