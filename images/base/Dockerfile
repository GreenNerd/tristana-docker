# NAME:    tristana/base
# VERSION: release
FROM ubuntu:16.04

MAINTAINER Phil Chen '06fahchen@gmail.com'

RUN echo 2.0.`date +%Y%m%d` > /VERSION

ENV RUBY_VERSION 2.3.1

RUN sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get update --fix-missing && apt-get -y upgrade

RUN apt-get -y install curl \
                       git-core \
                       build-essential \
                       redis-tools \
                       libpq-dev \
                       libssl-dev libreadline-dev zlib1g-dev \
                       nodejs \
                       nginx \
                       tzdata \
                       locales

RUN locale-gen en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

ENV RUBY_BUILD_MIRROR_URL=https://cache.ruby-china.org
RUN echo 'gem: --no-document' >> /usr/local/etc/gemrc && \
    mkdir /src && cd /src && \
    git clone https://github.com/sstephenson/ruby-build.git && \
    cd /src/ruby-build && \
    perl -p -i -e 's!cache.ruby-lang.org!cache.ruby-china.org!' './bin/ruby-build' && \
    perl -p -i -e 's!cache.ruby-lang.org!cache.ruby-china.org!' './share/ruby-build/2.3.1' && \
    ./install.sh && \
    cd / && rm -rf /src/ruby-build && \
    ruby-build $RUBY_VERSION /usr/local/

RUN gem update --system && gem cleanup

# clean up for docker squash
RUN   rm -fr /usr/share/man && \
      rm -fr /usr/share/doc && \
      rm -fr /usr/share/vim/vim74/tutor && \
      rm -fr /usr/share/vim/vim74/doc && \
      rm -fr /usr/share/vim/vim74/lang && \
      rm -fr /usr/local/share/doc && \
      rm -fr /usr/local/share/ruby-build && \
      rm -fr /root/.gem && \
      rm -fr /root/.npm && \
      rm -fr /tmp/* && \
      rm -fr /usr/share/vim/vim74/spell/en*

# Clean apt-get
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*
