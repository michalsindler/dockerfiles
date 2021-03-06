FROM ubuntu:xenial
MAINTAINER Michal Sindler docker [at] sindler [dot] net

# update package list
RUN apt-get update && \

# install curl and git
apt-get -y install curl git && \

# install php
apt-get -y install php7.0 mcrypt php7.0-mcrypt php-mbstring php-pear php7.0-dev php7.0-xml re2c gcc g++ && \

# install pre requisites
apt-get -y install apt-transport-https && \
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
apt-get update && \
ACCEPT_EULA=Y apt-get -y install msodbcsql mssql-tools && \
apt-get -y install unixodbc-dev && \
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile && \
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc && \

# install driver sqlsrv
pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system && \
pecl install sqlsrv && \
pecl install pdo_sqlsrv && \

# install locales
apt-get -y install locales && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen && \

# install apache
apt-get -y install libapache2-mod-php7.0 apache2 && \
a2dismod mpm_event && \
a2enmod mpm_prefork && \
a2enmod php7.0 && \
a2enmod rewrite && \
echo "extension=sqlsrv.so" >> /etc/php/7.0/apache2/php.ini && \
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini && \
service apache2 restart

WORKDIR myApp
EXPOSE 80