FROM php:7.2.12-fpm

# redis 版本
# ENV PHPREDIS_VERSION 3.1.6

# 安装composer
# COPY composer.phar /usr/local/bin/composer

# 换源文件
# COPY sources.list /etc/apt/china.sources.list

# 工作目录
WORKDIR /var/www/html

# 换源
# RUN rm /etc/apt/sources.list

# ADD sources.list /etc/apt/

# 扩展安装
RUN apt-get update\
    && apt-get install zlib1g-dev \
    && docker-php-ext-install mysqli pdo_mysql zip

# sqlsrv扩展安装
RUN rm /bin/sh && ln -s /bin/bash /bin/sh \
    && apt install -y gnupg apt-transport-https \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools \
    && echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile \
    && echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc \
    && /bin/bash -c "source ~/.bashrc" \
    && apt-get install -y unixodbc-dev \
    && pecl install sqlsrv \
    && pecl install pdo_sqlsrv \
    && pecl install redis