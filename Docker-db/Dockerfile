FROM mysql:5.7.25

LABEL maintainer="Rajaneesh Yembuluru"
LABEL description="MySQL database container for accounts service"
LABEL version="1.0"

ENV MYSQL_ROOT_PASSWORD=devopspassword
ENV MYSQL_DATABASE=accounts

COPY db_backup.sql /docker-entrypoint-initdb.d/db_backup.sql
EXPOSE 3306
