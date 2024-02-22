ARG IMAGE
FROM ${IMAGE}

USER root

ARG APT_PACKAGES="wget unzip ca-certificates curl gnupg gpg"
ARG APT_ADDITIONAL_PACKAGES=""
RUN apt-get update && apt-get upgrade -y && apt-get install -y ${APT_PACKAGES} ${APT_ADDITIONAL_PACKAGES} && rm -rf /var/lib/apt/lists/*

RUN wget -q -O /usr/local/bin/install-php-extensions https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions \
    || (echo "Failed while downloading php extension installer!"; exit 1)

ARG DATABASE_DRIVER
RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && install-php-extensions ${DATABASE_DRIVER} intl

ARG COMPOSER_VERSION=latest-stable
RUN wget "https://getcomposer.org/download/${COMPOSER_VERSION}/composer.phar" \
 && wget "https://getcomposer.org/download/${COMPOSER_VERSION}/composer.phar.sha256sum" \
 && sha256sum -c composer.phar.sha256sum \
 && rm composer.phar.sha256sum \
 && mv composer.phar /usr/local/bin/composer \
 && chmod +x /usr/local/bin/composer \
 && composer --version

ARG NODE_VERSION
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_VERSION}.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list
RUN apt-get update && apt-get install -y nodejs && rm -rf /var/lib/apt/lists/*
