FROM node:8-alpine
RUN  apk update &&  apk add git ca-certificates curl wget bash tzdata && \
        adduser node root && \
        mkdir -p /app && \
        chmod -R 775 /app && \
        chown -R node:root /app && \
        mkdir -p /.npm && \
        chmod -R 777 /.npm

RUN  yarn global add pm2 cross-env mocha node-gyp && \
     npm config set python /usr/bin/python2.7

ENV TZ=Asia/Tehran