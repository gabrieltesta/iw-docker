FROM php:5.6.31-apache
MAINTAINER Gabriel Testa <gabriel.testa.3@globalhitss.com.br>

# Altera sources dos repositórios do Debian 8 que foram depreciados
COPY sources.list /etc/apt/ 

# Configurações padrões do php.ini
COPY custom.ini /usr/local/etc/php/conf.d

# Instala dependências do php
RUN a2enmod rewrite && apt-get update && apt-get install --yes \ 
  ca-certificates git vim mariadb-client libpng12-dev libmcrypt-dev libmagic-dev libcurl4-openssl-dev && \
  docker-php-ext-install mysql mysqli pdo_mysql gd mcrypt mbstring 
  
# Cria vhosts para redirecionamento do IW
COPY env_conf/* 000-default.conf /etc/apache2/sites-available/
RUN a2ensite 000-default

# Instala composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php -r "if (hash_file('SHA384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/tmp/composer-setup.php'); } echo PHP_EOL;" && \
php composer-setup.php --install-dir=/usr/bin --filename=composer && \
php -r "unlink('composer-setup.php');"