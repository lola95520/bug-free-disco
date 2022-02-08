FROM debian:buster

LABEL version = "1" maintainer = "abonte-l <abonte-l@student.42.fr>"

ADD . /var/opt/

RUN apt-get update
RUN apt-get upgrade -y

EXPOSE 9000

RUN apt install -y \
	vim \
	wget \
	php7.3 php-mysql php-fpm php-cli php-mbstring 

RUN mkdir -p /var/www/html

COPY ./tools/wp-config.php /
COPY ./tools/wordpress.sql /var/

RUN tar xf ./wordpress.tar.gz \
&& rm -rf wordpress.tar.gz \
&& chmod 755 -R wordpress

RUN service php7.4-fpm start
COPY ./tools/www.conf /etc/php/7.3/fpm/pool.d/
COPY ./tools/php-fpm.conf /etc/php/7.3/fpm/

HEALTHCHECK --interval=30s --timeout=3s CMD --fail https://127.0.0.1/ || exit 1
CMD /usr/sbin/apache2ctl -D FOREGROUND
