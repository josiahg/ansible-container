FROM ubuntu:trusty

# Uses shell module - should be two tasks
RUN apt-get update -y && \
    apt-get install -y apache2 && \
    chown -R www-data /var/log/apache2 && \
    mkdir -p /run/apache2 && \
    chown -R www-data /run/apache2

# Install dumb-init from URL - get_url module
ADD https://github.com/Yelp/dumb-init/releases/download/v1.0.2/dumb-init_1.0.2_amd64 /usr/sbin/dumb-init

# Install httpd.conf - copy module
ADD trusty/ports.conf /etc/apache2/ports.conf

# Install heartbeat page - unarchive module
ADD html.tar.gz /var/www/html/

# Install chaff - synchronize module
COPY foo /

# Uses command module
RUN ["chmod", "755", "/usr/sbin/dumb-init"]

# I am defaults
ARG apache_port=8000
ENV APACHE_PORT=${apache_port}

# Single label
LABEL a=1
# Multiple labels
LABEL b=2 c=3
# Quoted keys and values
LABEL "the bird"="the word"
# Multi-line
LABEL foo=bar \
      baz=buzz

# I am metadata
CMD ["/usr/sbin/apache2", "-DFOREGROUND"]
ENTRYPOINT ["/usr/sbin/dumb-init"]
EXPOSE $apache_port
USER www-data
VOLUME ["/vol"]
WORKDIR /tmp
SHELL ["/bin/sh", "-c"]

# Should be run using shell module as www-data in /tmp explicitly using /bin/sh -c
# RUN /bin/true

