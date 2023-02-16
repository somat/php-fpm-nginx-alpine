FROM php:8.1.16-fpm-alpine

RUN apk add --no-cache supervisor nginx

COPY supervisord-app.conf /etc/supervisord.conf
COPY zzzz-docker.conf /usr/local/etc/php-fpm.d/zzzz-docker.conf
COPY default.conf /etc/nginx/http.d/default.conf

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
