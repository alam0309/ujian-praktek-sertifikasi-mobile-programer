FROM alpine:3.18

# Aktifkan community repo
RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories
RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories
RUN apk update 
RUN apk upgrade musl
RUN apk add --no-cache  \
    php81 \
    php81-openssl \
    php81-pdo_mysql \
    php81-mbstring \
    php81-fpm \
    php81-mysqli \
    php81-opcache \
    php81-json \
    php81-session \
    nginx \
    supervisor


# Buat direktori yang dibutuhkan
RUN mkdir -p /run/nginx /var/www/html

# Copy konfigurasi dan file
COPY ./nginx/default.conf /etc/nginx/http.d/default.conf
COPY ./supervisord.conf /etc/supervisord.conf
COPY ./src/index.php /var/www/html/index.php

EXPOSE 80

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]