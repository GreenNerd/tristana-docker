# NAME:    tristana/base
# VERSION: release

FROM tristana/base:2.3.1-ubuntu
MAINTAINER Phil Chen '06fahchen@gmail.com'

# specific bits
RUN useradd tristana -s /bin/bash -m -U && \
    mkdir -p /var/www/tristana/vendor/bundle \
    mkdir -p /var/www/tristana/vendor/gems

WORKDIR /var/www/tristana
RUN chown -R tristana:tristana /var/www/tristana

COPY tristana /var/www/tristana

RUN bundle config mirror.https://rubygems.org https://gems.ruby-china.org && \
    bundle install --deployment --without test development -j4 && \
    find /var/www/tristana/vendor/bundle -name tmp -type d -exec rm -rf {} +

RUN rm -rf /var/www/tristana/tmp/*
USER root
