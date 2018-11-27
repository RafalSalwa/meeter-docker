FROM ubuntu:16.04

# Enable php5.6 in ubuntu
RUN touch /etc/apt/sources.list.d/ondrej-php5.list && \
    echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list.d/ondrej-php5.list && \
    echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list.d/ondrej-php5.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C

RUN apt update && \
    apt install -y \
    apt-utils \
    tzdata \
    sudo \
    git \
    git-flow \
    vim \
    curl \
    supervisor \
    php7.2 \
    php7.2-common \
    php7.2-fpm \
    php7.2-intl \
    php7.2-mysql \
    php7.2-bcmath \
    php7.2-curl \
    php7.2-json \
    php7.2-readline \
    php7.2-zip \
    php7.2-opcache \
    php7.2-dev \
    php7.2-mbstring \
    php7.2-xml \
    php7.2-cli \
    php7.2-gd \
    php7.2-soap \
    mcrypt \
    nginx \
    bash-completion \
    mysql-client \
    && \
    # install nodejs
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    npm install --global pm2 yarn grunt && \
    # create local user and allow sudo without password
    useradd -ms /bin/bash limango && \
    usermod -aG www-data limango && \
    ((echo "limango ALL=(ALL) NOPASSWD:ALL" | tee -a /etc/sudoers) || true) && \
    # create php-fpm7.0 runtime directory
    mkdir /run/php

# set proper timezone
ENV TZ=Europe/Warsaw
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime
RUN echo $TZ > /etc/timezone

RUN curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin/ --filename=composer && \
    chmod +x /usr/local/bin/composer

RUN chown limango:limango -R /home/limango

USER limango
WORKDIR /var/www/
#CMD ["/sbin/init"]
CMD ["/bin/bash", "-c", "sudo supervisord --nodaemon"]
