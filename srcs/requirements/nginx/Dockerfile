FROM debian:bullseye

RUN apt-get update && apt-get install -y nginx openssl && \
	 rm -rf /var/lib/apt/lists/*

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/myagiz.42.fr.key -out /etc/ssl/certs/myagiz.42.fr.crt -subj "/C=TR/ST=KOCAELI/L=GEBZE/O=42Kocaeli/CN=myagiz.42.fr"

COPY ./conf/default.conf /etc/nginx/sites-available/default

CMD [ "nginx", "-g", "daemon off;"]

EXPOSE 443
