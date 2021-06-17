FROM       ubuntu:20.04
MAINTAINER siya Lai <siya891202@gmail.com> <siya891202@163.com>

ENV DEBIAN_FRONTEND=noninteractive
RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y net-tools software-properties-common && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && \
    apt-get install -y apt-transport-https zip mcrypt && \
    apt-get install -y libpq-dev libfreetype6-dev libmcrypt-dev && \
    apt-get install -y libcurl4-openssl-dev pkg-config libssl-dev openssh-server vim libncurses5-dev && \
    apt-get install -y ncurses-dev libreadline6-dev lua5.1-0-dev ruby ruby-dev python-dev libyaml-cpp-dev zlib1g.dev && \
    apt-get install -y curl tzdata && \
    apt-get install -y language-pack-zh-hant-base language-pack-zh-hans-base
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN echo "set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1" >> ~/.vimrc && \
    echo "set termencoding=utf-8" >> ~/.vimrc && \
    echo "set fileformats=unix" >> ~/.vimrc && \
    echo "set encoding=prc" >> ~/.vimrc

RUN echo "alias vi=vim" >> ~/.bashrc
RUN mkdir -p ~/.vim/bundle/vim-go ~/.vim/bundle/Vundle.vim
ADD vim-go /root/.vim/bundle/vim-go
ADD Vundle.vim /root/.vim/bundle/Vundle.vim
WORKDIR /data
ADD Dockerfile /data
RUN mkdir -p /var/run/sshd

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22
