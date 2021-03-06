FROM php:5.6-fpm

# Install libs
RUN apt-get update && apt-get install -y \
	libmcrypt-dev  \
	libicu-dev \
	mysql-client \
	zlib1g-dev \
	&& docker-php-ext-install pdo_mysql \
 		iconv \
 		mcrypt \
		intl \
 		opcache \
		mbstring \
		zip

# php gd
RUN apt-get update -y && apt-get install -y \
 	libpng-dev \
	&& docker-php-ext-install gd


# php soap
RUN apt-get update -y && apt-get install -y \
    libxml2-dev \
    php-soap \
  	&& apt-get clean -y \
  	&& docker-php-ext-install soap


# xDebug
RUN apt-get update -y && apt-get install -y \
 	&& pecl install xdebug  \
    && docker-php-ext-enable xdebug

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini


# Install mailhog.
RUN curl -fSL "https://github.com/mailhog/MailHog/releases/download/v1.0.0/MailHog_linux_amd64" -o /usr/local/bin/mailhog \
    && chmod +x /usr/local/bin/mailhog

COPY ./mailhog.ini /usr/local/etc/php/conf.d/mailhog.ini


CMD ["php-fpm"]