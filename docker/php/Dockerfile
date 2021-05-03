FROM php:7.4.3-fpm-alpine

RUN apk add --no-cache libzip-dev bash

VOLUME /var/www/html

COPY mongodburi.php /var/www/html/mongodburi.php
COPY mongodburi-entrypoint /usr/local/bin/mongodburi-entrypoint

RUN chmod +x /usr/local/bin/mongodburi-entrypoint

ENTRYPOINT ["mongodburi-entrypoint"]
CMD [ "php-fpm", "--allow-to-run-as-root", "--nodaemonize" ]
