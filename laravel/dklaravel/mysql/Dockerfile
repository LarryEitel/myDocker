FROM mysql:latest

MAINTAINER Larry Eitel <larry@eitel.com>

# ADD my.cnf /etc/mysql/conf.d/my.cnf
# ADD ./schema.sql /docker-entrypoint-initdb.d

# runs: /usr/local/bin/docker-entrypoint.sh
CMD ["mysqld"]

EXPOSE 3306

# The following is an alternative to initializing db
##! /bin/bash
#
## Grab full name of mysql container
#DB_CONTAINER=$(docker-compose ps | grep mysql | cut -d" " -f 1)
#
#docker exec -i $DB_CONTAINER mysql -uroot -proot < mysql/sites/cpo/schema.sql
#docker exec -i $DB_CONTAINER mysql -uroot -proot -e"show databases"
