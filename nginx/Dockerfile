FROM nginx

LABEL version="1.0"
LABEL name="Nginx"
LABEL description="Nginx with openssl. Start command override by docker-compose."

ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /

# generate self signed ssl cert
RUN apt-get update \
  && apt-get install -y --no-install-recommends openssl \
  && mkdir /etc/nginx/ssl \
  && openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt \
  -subj "/C=GB/ST=London/L=London/O=Global Security/OU=IT Department/CN=example.com" \
  && apt-get clean \
  && chmod +x /wait-for-it.sh