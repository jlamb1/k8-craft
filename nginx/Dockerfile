FROM nginx:latest

RUN apt-get update && \
    apt-get install -y postgresql-client-11

COPY app/ /var/www/html/

ADD nginx/default.conf /etc/nginx/conf.d/default.conf

RUN sed -ie "/user .* nginx;/d" /etc/nginx/nginx.conf \
    && echo "user root;" >> /etc/nginx/nginx.conf

# RUN chown -Rf nginx:nginx /var/www/html/

RUN mkdir -p /var/www/html/web/cpresources && \
    chmod -R 777 /var/www/html/config/ /var/www/html/storage/ /var/www/html/web/cpresources

EXPOSE 80