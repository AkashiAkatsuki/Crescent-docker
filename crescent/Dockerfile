FROM ruby
MAINTAINER AkashiAkatsuki

ENV APP_ROOT /usr/local/src/Crescent

RUN apt-get update && apt-get install -y git mecab libmecab-dev mecab-ipadic-utf8 make curl xz-utils file sudo wget apt-utils locales

RUN sed -i -e 's/# ja_JP.UTF-8/ja_JP.UTF-8/g' /etc/locale.gen && \
    locale-gen ja_JP.UTF-8

ENV LANG ja_JP.UTF-8
ENV LC_TIME C

#RUN git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git\
#    && cd mecab-ipadic-neologd\
#    && bin/install-mecab-ipadic-neologd -n -y

RUN git clone https://github.com/AkashiAkatsuki/Crescent $APP_ROOT
WORKDIR $APP_ROOT

COPY ./config ./config
RUN bundler
