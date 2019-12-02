FROM nginx:latest

# RUN wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
#     sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list' && \
RUN apt-get update && \
    apt-get install -y postgresql-client-11

COPY app /usr/share/nginx/

ADD ./nginx/default.conf /etc/nginx/conf.d/default.conf

RUN sed -ie "/user .* nginx;/d" /etc/nginx/nginx.conf \
    && echo "user root;" >> /etc/nginx/nginx.conf

RUN chown -Rf nginx:nginx /usr/share/nginx/

EXPOSE 80