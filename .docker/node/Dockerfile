FROM node:12-alpine

RUN apk --update upgrade && \
    apk add --update inotify-tools && \
    yarn && \
    rm -rf /var/cache/apk/*

WORKDIR /var/www/app

CMD ["yarn", "encore", "dev"]
EXPOSE 3000
