FROM wyveo/nginx-php-fpm:php73

# LABEL maintainer colin@wyveo.com

# Remove existing webroot, configure PHP session handler for Redis, install postgresql-client (pg_dump)
RUN rm -rf /usr/share/nginx/* && \
    sed -i -e "s/memory_limit\s*=\s*.*/memory_limit = 256M/g" ${php_conf} && \
    sed -i -e "s/max_execution_time\s*=\s*.*/max_execution_time = 120/g" ${php_conf} && \
    sed -i -e "s/session.save_handler\s*=\s*.*/session.save_handler = redis/g" ${php_conf} && \
    sed -i -e "s/;session.save_path\s*=\s*.*/session.save_path = tcp:redis-master:6379/g" ${php_conf} && \
    wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list' && \
    apt-get update && \
    apt-get install -y postgresql-client-11


COPY app /usr/share/nginx/

# Install the yii2-redis library
# RUN composer require --prefer-dist yiisoft/yii2-redis -d /usr/share/nginx/

# Add default craft cms nginx config
ADD ./nginx/default.conf /etc/nginx/conf.d/default.conf

RUN chown -Rf nginx:nginx /usr/share/nginx/

EXPOSE 80