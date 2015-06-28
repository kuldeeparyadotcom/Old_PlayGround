FROM ubuntu:14.04
MAINTAINER kd <kuldeeparyadotcom@gmail.com>
RUN apt-get update && apt-get install -y openssh-server 
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config.original
RUN chmod a-w /etc/ssh/sshd_config.original
RUN apt-get update && sudo apt-get install -y node.js npm wget vim git && sudo npm install -g bower
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN bower --allow-root install bootstrap
RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN apt-get update && apt-get -y install apache2 supervisor
RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/supervisor

#RUN mkdir /var/lock/apache2
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

VOLUME ["/var/www/html"]

CMD ["/usr/bin/supervisord"]

EXPOSE 22
EXPOSE 80
