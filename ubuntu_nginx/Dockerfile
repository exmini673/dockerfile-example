FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y nginx git
<<<<<<< HEAD
RUN git clone https://github.com/AnByoungHyun/static-web-template.git
COPY sites-available/default /etc/nginx/sites-available/default
RUN cp -r static-web-template/* /usr/share/nginx/html/
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
=======
RUN git clone https://github.com/exmini673/static-web-template.git
COPY sites-available/default /etc/nginx/sites-available/default
RUN cp -r static-web-template/* /usr/share/nginx/html/
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
>>>>>>> 38ad1818cd0543983fa7ed7b8c0faf2e665ca87b
