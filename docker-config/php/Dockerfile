FROM php:8-fpm
WORKDIR /var/www/html

RUN apt-get update

RUN apt-get -y install git vim build-essential libldap2-dev

RUN docker-php-ext-install bcmath ctype fileinfo ldap opcache pdo tokenizer

RUN apt-get -y install libxml2-dev

RUN docker-php-ext-install xml

RUN apt-get -y install libzip-dev

RUN docker-php-ext-install zip
#    && docker-php-ext-enable bcmath ctype fileinfo ldap opcache pdo tokenizer xml zip

# RUN docker-php-ext-install openssl && docker-php-ext-enable openssl

RUN pecl install mongodb && docker-php-ext-enable mongodb

RUN cd ~; php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \    
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

RUN echo export PATH=$PATH:/root/.composer/bin >> /etc/bash.bashrc