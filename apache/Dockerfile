FROM ubuntu:24.04 AS cliente_git
RUN apt update && apt install -y git
RUN git clone https://github.com/deaw-birt/UD4-despliegue-PHP.git

FROM ubuntu:18.04

RUN apt-get update && apt-get install -y apache2 \
    && apt-get -y install libapache2-mod-fcgid \
    && a2enmod proxy_fcgi

COPY 000-default.conf /etc/apache2/sites-available
COPY --from=cliente_git UD4-despliegue-PHP/php/* /var/www/html/
COPY --from=cliente_git UD4-despliegue-PHP/mysql/crearBBDD.sql /mysql-scripts/01.crearBBDD.sql
COPY --from=cliente_git UD4-despliegue-PHP/mysql/InsertarDatos.sql /mysql-scripts/02.InsertarDatos.sql 

EXPOSE 80
CMD ["apachectl", "-D", "FOREGROUND"]
