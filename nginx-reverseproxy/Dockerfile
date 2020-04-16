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

RUN ln -s /etc/nginx/sites-available/ww2.admin.edujob.com.br.conf /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/ww2.api-basic.edujob.com.br.conf /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/ww2.api.edujob.com.br.conf /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/ww2.candidato.edujob.com.br.conf /etc/nginx/sites-enabled/


COPY otherconf/supervisord.conf /etc/supervisor/supervisord.conf

RUN mkdir -p /etc/letsencrypt/live/ww2.admin.edujob.com.br/
COPY ssl/ww2.admin.edujob.com.br/*.pem /etc/letsencrypt/live/ww2.admin.edujob.com.br/

RUN mkdir -p /etc/letsencrypt/live/ww2.candidato.edujob.com.br/
COPY ssl/ww2.candidato.edujob.com.br/*.pem /etc/letsencrypt/live/ww2.candidato.edujob.com.br/

#ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
COPY start.sh /start.sh
CMD ["./start.sh"]
