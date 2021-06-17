FROM siya/ubuntu20.04-vim-ssh
MAINTAINER siya Lai <siya891202@gmail.com> <siya891202@163.com>

ADD Dockerfile /data
WORKDIR /data
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 && \
    LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/nginx && \
    echo "deb http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" | tee /etc/apt/sources.list.d/nginx.list && \
    apt-key fingerprint ABF5BD827BD9BF62
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y nginx git cron supervisor librabbitmq-dev
RUN apt-get install -y php5.6 php5.6-common php5.6-fpm php5.6-dev && \
    apt-get install -y php5.6-mbstring php5.6-xml php5.6-gd php5.6-exif php5.6-zip php5.6-iconv php5.6-bcmath php5.6-mcrypt php5.6-pgsql php5.6-mysql php5.6-redis php5.6-mongo php5.6-amqp php5.6-curl && \
    apt-get install -y php7.1 php7.1-common php7.1-fpm php7.1-dev && \
    apt-get install -y php7.1-mbstring php7.1-xml php7.1-gd php7.1-exif php7.1-zip php7.1-iconv php7.1-bcmath php7.1-mcrypt php7.1-pgsql php7.1-mysql php7.1-redis php7.1-mongo php7.1-amqp php7.1-curl && \
    apt-get install -y php7.2 php7.2-common php7.2-fpm php7.2-dev && \
    apt-get install -y php7.2-mbstring php7.2-xml php7.2-gd php7.2-zip php7.2-bcmath php7.2-pgsql php7.2-mysql php7.2-redis php7.2-mongodb php7.2-amqp php7.2-curl && \
    apt-get install -y php7.3 php7.3-common php7.3-fpm php7.3-dev && \
    apt-get install -y php7.3-mbstring php7.3-xml php7.3-gd php7.3-zip php7.3-bcmath php7.3-pgsql php7.3-mysql php7.3-redis php7.3-mongodb php7.3-amqp php7.3-curl && \
    apt-get install -y php7.4 php7.4-common php7.4-fpm php7.4-dev && \
    apt-get install -y php7.4-mbstring php7.4-xml php7.4-gd php7.4-zip php7.4-bcmath php7.4-pgsql php7.4-mysql php7.4-redis php7.4-mongodb php7.4-amqp php7.4-curl && \
    apt-get install -y php8.0 php8.0-common php8.0-fpm php8.0-dev && \
    apt-get install -y php8.0-mbstring php8.0-xml php8.0-gd php8.0-zip php8.0-bcmath php8.0-pgsql php8.0-mysql php8.0-redis php8.0-mongodb php8.0-amqp php8.0-curl && \
    rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/*
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | tee /usr/share/keyrings/yarnkey.gpg >/dev/null && \
    echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y nodejs && \
    apt-get install -y yarn && \
    npm install -g cnpm --registry=https://registry.npm.taobao.org && \
    php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    rm -rf /tmp/* && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /data/src && cd /data/src && \
    wget https://dl.google.com/go/go1.12.6.linux-amd64.tar.gz && tar -zxvf go1.12.6.linux-amd64.tar.gz

RUN ln -f /data/src/go/bin/go /usr/local/bin/go && ln -f /data/src/go/bin/gofmt /usr/local/bin/gofmt && ln -f /data/src/go/bin/godoc /usr/local/bin/godoc && \
    export GOROOT=/data/src/go && export GOPATH=/data/src/ && echo "PATH=\$PATH:/usr/local/bin" >> /root/.bashrc && echo "PATH=\$PATH:\$GOROOT/bin" >> /root/.bashrc

RUN sed -i "s/\/run\/php\/php7.1-fpm.sock/127.0.0.1:9000/g" /etc/php/7.1/fpm/pool.d/www.conf && \
    mkdir -p /run/php/ && ln -s /usr/sbin/php-fpm7.1 /usr/sbin/php-fpm

RUN echo "【php version】" && php -v && \
    echo "【nginx version】" && nginx -v && \
    echo "【supervisor version】" && /usr/bin/supervisord -v && \
    echo "【nodejs version】" && node -v && \
    echo "【npm version】" && npm -v && \
    echo "【cnpm version】" && cnpm -v && \
    echo "【yarn version】" && yarn -v && \
    echo "【composer version】" && composer --version && \
    echo "【php modules】" && php -m
ENV TZ=Asia/Shanghai