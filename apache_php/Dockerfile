# apache & php example
FROM ubuntu
MAINTAINER Slawek

RUN apt-get update && \ 
	apt-get install -y apache2 vim nano php7.0 php7.0-fpm php7.0-mysql php7.0-cli && \
	apt-get clean && \ 
	rm -rf /var/lib/apt/lists/*

RUN echo "<?php  phpinfo() ?>" > /var/www/html/infophp.php

EXPOSE 80

CMD apachectl -D FOREGROUND 
