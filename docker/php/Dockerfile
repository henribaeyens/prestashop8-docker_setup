ARG IMAGE
FROM ${IMAGE}

# Install packages
ARG APT_PACKAGES="wget unzip curl gpg"
ARG APT_ADDITIONAL_PACKAGES=""
RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y ${APT_PACKAGES} ${APT_ADDITIONAL_PACKAGES} \
 && rm -rf /var/lib/apt/lists/*

# download helper script
RUN wget -q -O /usr/local/bin/install-php-extensions https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions \
    || (echo "Failed while downloading php extension installer!"; exit 1)

ARG DATABASE_DRIVER
RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && install-php-extensions \
    ${DATABASE_DRIVER} intl

ARG NODE_VERSION
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_VERSION}.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list
RUN apt-get update \
 && apt-get install -y nodejs \
 && rm -rf /var/lib/apt/lists/*
