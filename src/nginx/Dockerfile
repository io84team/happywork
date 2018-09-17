FROM nginx:alpine
MAINTAINER Aben <aben@abenx.com>

COPY nginx.conf /etc/nginx/

RUN apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data

# Remove the default conf
RUN rm /etc/nginx/conf.d/default.conf

CMD ["nginx"]

EXPOSE 80 443
