# FROM docker.io/centos:7
#
# ENV NGINX_VERSION="1.13.4-1.el7"
#
# # Add NGINX repo to yum
# ADD nginx.repo /etc/yum.repos.d/nginx.repo
#
# # Install NGINX
# RUN curl -sO http://nginx.org/keys/nginx_signing.key && \
#     rpm --import ./nginx_signing.key && \
#     yum -y install --setopt=tsflags=nodocs nginx-${NGINX_VERSION}.ngx && \
#     rm -f ./nginx_signing.key && \
#     yum clean all
#
# # Forward request and error logs to docker log collector
# RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
#     ln -sf /dev/stderr /var/log/nginx/error.log && \
# # Change pid file location & remove nginx user & change port to 8080
#     sed -i 's/\/var\/run\/nginx.pid/\/var\/cache\/nginx\/nginx.pid/g' /etc/nginx/nginx.conf && \
#     sed -i -e '/user/!b' -e '/nginx/!b' -e '/nginx/d' /etc/nginx/nginx.conf && \
#     sed -i -e '/listen/!b' -e '/80;/!b' -e 's/80;/8080;/' /etc/nginx/conf.d/default.conf && \
# # Modify perms for non-root runtime
#     chown -R 998 /var/cache/nginx /etc/nginx && \
#     chmod -R g=u /var/cache/nginx /etc/nginx
#
# VOLUME ["/var/cache/nginx"]
#
# EXPOSE 8080 8443
#
# USER 998
#
# CMD ["nginx", "-g", "daemon off;"]

FROM nginx

RUN chmod 777 /var/cache/nginx \
    && sed -i -e '/listen/!b' -e '/80;/!b' -e 's/80;/8080;/' /etc/nginx/conf.d/default.conf \
    && sed -i 's!/var/run/nginx.pid!/var/cache/nginx/nginx.pid!g' /etc/nginx/nginx.conf
