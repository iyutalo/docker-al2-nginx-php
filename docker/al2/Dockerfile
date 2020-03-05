FROM amazonlinux:2

SHELL ["/bin/bash", "-c"]

RUN yum update -y && \
    yum clean all

RUN yum install -y wget man git gcc-c++ make sudo vim python3 net-tools

RUN curl -sL https://rpm.nodesource.com/setup_12.x | sudo -E bash - && \
    yum install -y nodejs && \
    amazon-linux-extras install nginx1 && \
    amazon-linux-extras install -y php7.3 && \
    amazon-linux-extras enable php7.3 && \
    yum install -y php-mbstring php-opcache
RUN \
    systemctl enable php-fpm.service && \
    systemctl enable nginx.service


COPY ./etc/php.ini /etc/php.ini
COPY ./etc/php-fpm.d/www.conf /etc/php-fpm.d/www.conf
COPY ./etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY ./etc/nginx/default.d/security.conf /etc/nginx/default.d/security.conf
COPY ./etc/nginx/nginx.conf /etc/nginx/nginx.conf

RUN chown -R nginx.nginx /var/lib/php/session/

CMD ["/sbin/init"]
