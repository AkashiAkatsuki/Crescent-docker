FROM postgres

RUN apt-get update && \
    apt-get install -y apt-utils locales && \
    sed -i -e 's/# ja_JP.UTF-8/ja_JP.UTF-8/g' /etc/locale.gen && \
    locale-gen ja_JP.UTF-8

ENV LANG ja_JP.UTF-8
ENV LC_TIME C

ADD ./createdb.sql /docker-entrypoint-initdb.d/
