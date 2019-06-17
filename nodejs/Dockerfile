
FROM node:8-alpine
RUN  apk update && \
     apk add --no-cache --virtual .build-dependencies \
        binutils-gold \
        build-base \
        g++ \
        gcc \
        libgcc \
        libstdc++ \
        gnupg \
        libtool \
        autoconf \
        automake \
        jq \
        openssh \
        linux-headers \
        make \
        openssl \
        python

RUN  apk add git ca-certificates curl wget bash tzdata && \
        adduser node root && \
        mkdir -p /app && \
        chmod -R 775 /app && \
        chown -R node:root /app && \
        mkdir -p /.npm && \
        chmod -R 777 /.npm

RUN  yarn global add pm2 cross-env mocha node-gyp && \
     npm config set python /usr/bin/python2.7

ENV TZ=Asia/Tehran
