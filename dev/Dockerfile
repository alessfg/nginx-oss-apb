FROM docker.io/centos:7

MAINTAINER NGINX Docker Maintainers "docker-maint@nginx.com"

ADD nginx.repo /etc/yum.repos.d/nginx.repo

RUN curl -sO http://nginx.org/keys/nginx_signing.key && \
    rpm --import ./nginx_signing.key && \
    yum -y install --setopt=tsflags=nodocs nginx && \
    rm -f ./nginx_signing.key && \
    yum clean all

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \
# change pid file location & port to 8080
    sed -i -e '/pid/!b' -e '/\/var\/run\/nginx.pid/!b' -e '/\/var\/run\/nginx.pid/d' /etc/nginx/nginx.conf && \
    sed -i -e '/listen/!b' -e '/80;/!b' -e 's/80;/8080;/' /etc/nginx/conf.d/default.conf && \
# modify perms for non-root runtime
    chown -R 998 /var/cache/nginx && \
    chmod -R g=u  /var/cache/nginx

VOLUME ["/var/cache/nginx"]

EXPOSE 8080 8443

USER 998

CMD ["nginx", "-g", "daemon off; pid /var/cache/nginx/nginx.pid;"]
