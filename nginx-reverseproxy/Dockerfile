FROM ubuntu:18.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -yq install net-tools nginx supervisor && \
    useradd -ms /bin/bash aurora && \
    rm -f /etc/nginx/fastcgi.conf /etc/nginx/fastcgi_params && \
    rm -f /etc/nginx/snippets/fastcgi-php.conf /etc/nginx/snippets/snakeoil.conf
EXPOSE 80
EXPOSE 443
#COPY nginx/ssl /etc/nginx/ssl
#COPY nginx/snippets /etc/nginx/snippets
COPY *.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/api.appmoneygestor.com.br.conf /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/appmoneygestor.com.br.conf /etc/nginx/sites-enabled/


COPY otherconf/supervisord.conf /etc/supervisor/supervisord.conf

RUN mkdir -p /etc/letsencrypt/live/api.appmoneygestor.com.br/
COPY ssl/api.appmoneygestor.com.br/*.pem /etc/letsencrypt/live/api.appmoneygestor.com.br/

RUN mkdir -p /etc/letsencrypt/live/appmoneygestor.com.br/
COPY ssl/appmoneygestor.com.br/*.pem /etc/letsencrypt/live/appmoneygestor.com.br/

#ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
COPY start.sh /start.sh
CMD ["./start.sh"]
