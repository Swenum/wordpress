FROM ubuntu:bionic
LABEL maintainer "Uladzimir Schuka wetoster@gmail.com"

# Fixes some weird terminal issues such as broken clear / CTRL+L
ENV TERM=linux

# Ensure apt doesn't ask questions when installing stuff
ENV DEBIAN_FRONTEND=noninteractive

# Install Ondrej repos for Ubuntu Bionic, PHP7.4, composer and selected extensions - better selection than
# the distro's packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu bionic main" > /etc/apt/sources.list.d/ondrej-php.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        ca-certificates \
        curl \
        unzip \
        php-apcu \
        php-apcu-bc \
        php7.4-cli \
        php7.4-curl \
        php7.4-json \
        php7.4-mbstring \
        php7.4-opcache \
        php7.4-readline \
        php7.4-xml \
        php7.4-zip \
        php7.4-fpm\
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require hirak/prestissimo \
    && composer clear-cache \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* ~/.composer

STOPSIGNAL SIGQUIT

CMD ["/usr/sbin/php-fpm7.4", "-O" ]

EXPOSE 9000