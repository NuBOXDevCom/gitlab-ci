FROM resin/rpi-raspbian:stretch

MAINTAINER Sylvain B. For TIL2F

USER root

RUN echo "deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi" > /etc/apt/sources.list.d/custom.list

RUN apt update && apt dist-upgrade -y

RUN apt install -y apache2

RUN apt install -y htop wget make ca-certificates dpkg-dev gcc g++ locales tzdata

RUN mkdir -p /var/www/html

RUN chmod 777 -R /var/www/html && chown -R www-data:www-data /var/www/html

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_DOCUMENT_ROOT /var/www/html
ENV DEBIAN_FRONTEND noninteractive
ENV TIMEZONE Europe/Paris
ENV LANGUAGE fr_FR.UTF-8
ENV LANG fr_FR.UTF-8
ENV LC_ALL fr_FR.UTF-8

RUN locale-gen $LANGUAGE && \
    dpkg-reconfigure locales && \
    echo "$TIMEZONE" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata

RUN apt install -y php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-json php7.0-gd php7.0-mcrypt php7.0-intl php7.0-sqlite3 php7.0-gmp php7.0-mbstring php7.0-xml php7.0-zip php7.0-opcache php7.0-dev php7.0-bcmath php7.0-xsl php7.0-bz2 php7.0-enchant php7.0-imap php7.0-ldap php7.0-pgsql php7.0-pspell php7.0-readline php7.0-recode php7.0-soap php7.0-tidy php7.0-gd php7.0-intl php7.0-xmlrpc php7.0-common php7.0-cgi php7.0-cli php7.0-fpm php-pear php-xdebug php-memcache php-imagick php-apcu

RUN a2enmod actions alias allowmethods asis autoindex buffer cache cgi cgid deflate dir env expires filter headers http2 ident include mime mime_magic negotiation proxy proxy_fcgi proxy_http proxy_http2 proxy_scgi rewrite session session_cookie setenvif speling ssl vhost_alias

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
