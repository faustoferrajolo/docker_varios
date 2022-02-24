# docker_varios


PASOS

1- sudo sysctl -w vm.max_map_count=262144
2- ./init.sh
3- chown -R pgadmin:pgadmin pgadmin-data
   chown -R postgres:postgres db-data
   chown -R sonarqube:sonarqube sonarqube_*

Se puede revertir los cambios ejecutando delete_all.sh

'''init.sh

#!/bin/bash

groupadd -f -g 5050 pgadmin
groupadd -f -g 5051 postgres
groupadd -f -g 5052 sonarqube

useradd -u 5050 -g 5050 pgadmin
useradd -u 5051 -g 5051 postgres
useradd -u 5052 -g 5052 sonarqube

mkdir db-data
mkdir sonarqube_data
mkdir sonarqube_extensions
mkdir sonarqube_logs
mkdir pgadmin-data
mkdir sonarqube_extensions/plugins

chown -R pgadmin:pgadmin pgadmin-data
chown -R postgres:postgres db-data
chown -R sonarqube:sonarqube sonarqube_*

cd sonarqube_extensions/plugins
wget https://binaries.sonarsource.com/Distribution/sonar-auth-bitbucket-plugin/sonar-auth-bitbucket-plugin-1.1.0.381.jar


'''delete_all.sh

#!/bin/bash

rm -Rf db-data pgadmin-data sonarqube_*

userdel -f -r pgadmin
userdel -f -r postgres
userdel -f -r sonarqube

groupdel -f pgadmin
groupdel -f postgres
groupdel -f sonarqube


Correr docker compose
docker-compose up -d
