FROM nginx
COPY static-html-directory /usr/share/nginx/html

# To redirect logs so "docker logs" can be sent through gelf
#RUN ln -sf /dev/stdout /var/log/nginx/access.log
#RUN ln -sf /dev/stderr /var/log/nginx/error.log
