FROM debian:bullseye

RUN apt-get update && apt-get -y install php php-mysql php-fpm php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip curl mariadb-client sudo && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www/html

COPY ./conf/www.conf /etc/php/7.4/fpm/pool.d

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar --output /usr/bin/wp --silent

RUN chmod +x wp-cli.phar && mv wp-cli.phar /usr/bin/wp

RUN chmod +x /usr/bin/wp

RUN mkdir /run/php

COPY ./tool/script.sh /script.sh

RUN chmod +x /script.sh

EXPOSE 9000

CMD ["/script.sh"]
