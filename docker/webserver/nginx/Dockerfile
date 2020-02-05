FROM nginx

ADD ./conf/default.conf /etc/nginx/conf.d/default.conf

# Update apt-get
RUN apt-get update -qq

# Install nano and vim
RUN apt-get install -y nano \
    && nano --version \
    && apt-get install -y vim \
    && vi --version

WORKDIR /var/www/html