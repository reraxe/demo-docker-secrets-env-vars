FROM php:7.4.3-fpm-alpine

RUN apk add --no-cache libzip-dev bash

VOLUME /var/www/html

COPY mongodb.php /var/www/html/mongodb.php
COPY mongodb-entrypoint /usr/local/bin/mongodb-entrypoint

RUN chmod +x /usr/local/bin/mongodb-entrypoint

ENTRYPOINT ["mongodb-entrypoint"]
CMD [ "php-fpm", "--allow-to-run-as-root", "--nodaemonize" ]
