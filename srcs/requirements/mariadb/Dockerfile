FROM debian:buster

LABEL version = "1" maintainer = "abonte-l <abonte-l@student.42.fr>"

ADD . /var/opt/

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		mariadb-server \
		vim \
		sudo

COPY ./COPY/my.cnf /etc/mysql/my.cnf
COPY ./COPY/create_mariadb_admin_user.sh /usr/local/bin/create_mariadb_admin_user.sh

RUN chmod 777 /usr/local/bin/create_mariadb_admin_user.sh

ARG MYSQL_ROOT_PASSWORD
ARG MYSQL_PASSWORD
ARG MYSQL_USER
ENV WP_DB_NAME=${WP_DB_NAME}
ENV MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
ENV MYSQL_PASSWORD=${MYSQL_PASSWORD}
ENV MYSQL_USER=${MYSQL_USER}

EXPOSE 3306

RUN sh /usr/local/bin/create_mariadb_admin_user.sh

CMD ["mysqld_safe"]