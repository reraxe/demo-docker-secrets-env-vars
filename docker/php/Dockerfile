FROM php:7.4.3-fpm-alpine

RUN apk add --no-cache libzip-dev bash

VOLUME /var/www/html

COPY mongouri.php /var/www/html/mongouri.php
COPY mongouri-entrypoint /usr/local/bin/mongouri-entrypoint

RUN chmod +x /usr/local/bin/mongouri-entrypoint

ENTRYPOINT ["mongouri-entrypoint"]
CMD [ "php-fpm", "--allow-to-run-as-root", "--nodaemonize" ]
