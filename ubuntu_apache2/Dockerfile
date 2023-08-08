FROM ubuntu:focal
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y apache2
<<<<<<< HEAD
RUN git clone https://github.com/AnByoungHyun/static-web-template.git
=======
RUN git clone https://github.com/exmini673/static-web-template.git
>>>>>>> 38ad1818cd0543983fa7ed7b8c0faf2e665ca87b
RUN cp -r static-web-template/* /var/www/html/
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80