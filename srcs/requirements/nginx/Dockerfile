FROM debian:buster

LABEL version = "1" maintainer = "abonte-l <abonte-l@student.42.fr>"

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		nginx \
		openssl \
		curl \
		vim \
		sudo

COPY ./tools/nginx.conf /etc/nginx/nginx.conf
COPY ./tools/dafault /etc/nginx/sites-available/default

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -subj '/C=FR/ST=IDF/L=Paris/O=42/CN=abonte-l' -keyout /etc/ssl/certs/localhost.key -out /etc/ssl/certs/localhost.crt

HEALTHCHECK --interval=30s --timeout=3s CMD --fail https://127.0.0.1/ || exit 1
CMD [ "nginx", "-g", "daemon off;" ]