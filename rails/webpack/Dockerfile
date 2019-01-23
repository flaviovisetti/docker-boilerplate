FROM ruby:2.6.0-alpine

RUN set -x \
    && apk update \
    && apk upgrade --no-cache \
    && apk add --no-cache --virtual build-dependencies \
    build-base libc-dev linux-headers tzdata vim imagemagick \
    libressl postgresql-dev nodejs yarn \
    && apk add --no-cache \
    libxml2-dev \
    libxslt-dev \
    && gem install nokogiri \
    -- --use-system-libraries \
    --with-xml2-config=/usr/bin/xml2-config \
    --with-xslt-config=/usr/bin/xslt-config

WORKDIR /tmp
COPY Gemfile Gemfile.lock package.json yarn.lock ./
RUN yarn install && bundle install

WORKDIR /var/www/app
COPY . ./

EXPOSE 3000

CMD ["bundle exec puma -C config/puma.rb"]
