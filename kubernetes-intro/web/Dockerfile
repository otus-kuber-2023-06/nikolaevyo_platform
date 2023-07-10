FROM centos:centos7

RUN  mkdir /app/ \
    &&  yum -y install epel-release \
    &&  yum -y install nginx \
    &&  usermod -u 1001 nginx && groupmod -g 1001 nginx

ADD nginx.conf /etc/nginx/nginx.conf

EXPOSE 8000

CMD ["nginx", "-g", "daemon off;"]
