FROM mysql:8.0.33-debian
MAINTAINER Gabriel Testa <gabriel.testa.3@globalhitss.com.br>

ENV MYSQL_ROOT_PASSWORD=root \
    MYSQL_DATABASE=test \
    MYSQL_USER=iw \
    MYSQL_PASSWORD='iw' \
    TERM=xterm

EXPOSE 3306

COPY conf.d/* /etc/mysql/conf.d

VOLUME ["/var/lib/mysql"]