FROM php:8.2-fpm AS php-fpm

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd \
    && apt-get update && apt install -y libicu-dev libpq-dev libxml2-dev libzip-dev\
    && docker-php-ext-install intl pgsql pdo_pgsql pdo_mysql mysqli soap sockets bcmath zip\
	&& apt-get install -y git

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN echo "root:root" | chpasswd
COPY --from=composer:2.5 /usr/bin/composer /usr/local/bin/composer

RUN useradd --user-group --create-home developer
USER developer