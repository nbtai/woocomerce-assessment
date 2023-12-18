ARG php_version
FROM php:${php_version}-fpm

LABEL version="1.0"
LABEL name="PHP"
LABEL description="PHP with xdebug, phpunit, guzzle, composer and mailhog"

## build arguments, note: php_version gets reset after FROM, required again here
ARG php_version
ARG xdebug_remote_port

## PHPUNIT 6 uses namespaces, which messes with WP Test Suite
ENV GUZZLE_VERSION=6
ENV PHPUNIT_VERSION=5

## copy files from repository to container root
COPY php/entrypoint.sh php/wp-cli.template.yml php/index.php /
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /

## install the PHP extensions we need
RUN apt-get update \
  && apt-get install -y --no-install-recommends unzip subversion dos2unix msmtp \
  && rm -rf /var/lib/apt/lists/* \
  && \
    if [ "${php_version%%.*}" -lt "7" ]; then \
      pecl install xdebug-2.5.5; \
    else \
      pecl install xdebug-3.1.5; \ 
    fi \
  && docker-php-ext-enable xdebug \
  && docker-php-ext-install mysqli \
  && apt-get clean

## install composer and wp-cli
ENV PATH /root/.composer/vendor/bin:$PATH
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/bin \
  && composer global require guzzlehttp/guzzle ^${GUZZLE_VERSION} \
  && composer global require phpunit/phpunit ^${PHPUNIT_VERSION} \
  && phpunit --version \
  && curl -o /usr/local/bin/wp -SL https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod +x /usr/local/bin/wp \
  && wp --info --allow-root \
  && dos2unix /entrypoint.sh \
  && chmod +x /entrypoint.sh \
  && chmod +x /wait-for-it.sh

##
ENTRYPOINT ["/entrypoint.sh"]
CMD ["php-fpm"]
