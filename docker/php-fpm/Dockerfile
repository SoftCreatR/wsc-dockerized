FROM php:8.1-fpm-alpine AS base
LABEL maintainer="Sascha Greuel <sascha@softcreatr.de>"

RUN set -eux; \
    apk add --no-cache \
        bash=~5.1.16 \
        curl=~7.83.1 \
        libxml2-dev=~2.9.14 \
        tar=~1.34 \
        imagemagick=~7 \
;

# Configure & Install PHP extensions
RUN set -eux; \
    curl -sL https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions -o /usr/local/bin/install-php-extensions \
    && chmod +x /usr/local/bin/install-php-extensions \
    && IPE_GD_WITHOUTAVIF=1 install-php-extensions \
        exif \
        intl \
        gd \
        gmp \
        imagick \
        pdo_mysql \
        redis \
;

FROM base AS final

# Setup entrypoint and start
COPY ./start-container.sh /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

ENTRYPOINT ["start-container", "/wsc", "5.5"]
