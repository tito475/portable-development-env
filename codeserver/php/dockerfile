# codeserver/php/Dockerfile
FROM linuxserver/code-server:latest

RUN \
  echo "**** install runtime dependencies ****" && \
  apt-get update && \
  apt-get install -y \
    php8.2 \
    php8.2-cli \
    php8.2-common \
    php8.2-curl \
    php8.2-mbstring \
    php8.2-mysql \
    php8.2-xml \
    php8.2-zip \
    php8.2-gd \
    php8.2-sqlite3 \
    php8.2-bcmath \
    php8.2-intl \
    php8.2-soap \
    php8.2-xdebug \
    php8.2-dev \
    unzip \
    curl \
    wget \
    git \
    sudo && \
  echo "**** install Composer ****" && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
  echo "**** install Node.js (for modern PHP development tools) ****" && \
  curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && \
  apt-get install -y nodejs && \
  echo "**** configure PHP ****" && \
  echo "memory_limit = 256M" >> /etc/php/8.2/cli/php.ini && \
  echo "max_execution_time = 300" >> /etc/php/8.2/cli/php.ini && \
  echo "upload_max_filesize = 64M" >> /etc/php/8.2/cli/php.ini && \
  echo "post_max_size = 64M" >> /etc/php/8.2/cli/php.ini && \
  echo "**** install global PHP tools ****" && \
  composer global require laravel/installer && \
  composer global require symfony/cli && \
  composer global require phpunit/phpunit && \
  composer global require squizlabs/php_codesniffer && \
  composer global require friendsofphp/php-cs-fixer && \
  echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> /etc/bash.bashrc && \
  echo "**** clean up ****" && \
  apt-get clean && \
  rm -rf \
    /config/* \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*

# Configure Xdebug for development
RUN echo "zend_extension=xdebug.so" >> /etc/php/8.2/cli/php.ini && \
    echo "xdebug.mode=debug,develop" >> /etc/php/8.2/cli/php.ini && \
    echo "xdebug.start_with_request=yes" >> /etc/php/8.2/cli/php.ini && \
    echo "xdebug.client_host=host.docker.internal" >> /etc/php/8.2/cli/php.ini && \
    echo "xdebug.client_port=9003" >> /etc/php/8.2/cli/php.ini

# Add composer global bin to PATH for all users
RUN echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> /etc/profile

# ports and volumes
EXPOSE 8443