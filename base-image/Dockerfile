FROM php:7.4-apache

COPY wp-config.php wp-config.php

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions \
        bcmath \
		exif \
		gd \
		mysqli \
		zip

RUN set -eux; \
	version='5.8.1'; \
	sha1='21e50add5a51cd9a18610244c942c08f7abeccd8'; \
	\
	curl -o wordpress.tar.gz -fL "https://wordpress.org/wordpress-$version.tar.gz"; \
	echo "$sha1 *wordpress.tar.gz" | sha1sum -c -; \
	\
# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
	tar -xzf wordpress.tar.gz; \
	rm wordpress.tar.gz; \
    cp -r wordpress/* .

VOLUME /var/www/html/wp-content