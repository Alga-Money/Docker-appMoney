FROM nginx:stable-alpine
#COPY *.conf /etc/nginx/conf.d/
RUN apk add supervisor 
copy *.conf /etc/nginx/conf.d/
copy index.html /usr/share/nginx/html/
EXPOSE 80/tcp
EXPOSE 443/tcp
#CMD ["nginx", "-g", "daemon off;"]
copy otherconf/supervisord.conf /etc/supervisor/supervisord.conf
#ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
COPY start.sh /start.sh
CMD ["./start.sh"]
