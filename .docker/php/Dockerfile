FROM php:7.4.10-fpm-alpine

# installation de git
RUN apk add --no-cache --update git \
    && rm -rf /tmp/*

# copie du script php-extension-installer depuis l'image docker
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin
# ce script facilite l'installation d'extensions php non standard
# pour vérifier quels modules sont installés dans l'image de base, lancer la commande `docker run --rm php:7.4.10-alpine php -m`
RUN install-php-extensions gd apcu opcache memcache pdo_mysql

# COPY php.custom.ini /usr/local/etc/php/conf.d/app_custom.ini

# copie de composer depuis l'image docker
COPY --from=composer /usr/bin/composer /usr/bin/composer

# copie de symfony cli depuis l'image docker
COPY --from=symfonycorp/cli /symfony /usr/bin/symfony

WORKDIR /var/www/app

#RUN rm src/.gitkeep

RUN git config --global user.name "Greg Berger" \
    && git config --global user.email "greg@3kd.be"

CMD ["php-fpm"]

EXPOSE 9000
