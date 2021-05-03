FROM php:7.4.3-fpm-alpine

RUN apk add --no-cache libzip-dev bash

VOLUME /var/www/html

COPY mongouri.php /var/www/html/mongouri.php
COPY CHANGETHIS-entrypoint /usr/local/bin/CHANGETHIS-entrypoint

RUN chmod +x /usr/local/bin/CHANGETHIS-entrypoint

ENTRYPOINT ["CHANGETHIS-entrypoint"]
CMD [ "php-fpm", "--allow-to-run-as-root", "--nodaemonize" ]
