FROM php-fpm-dev

ENV LD_LIBRARY_PATH /usr/local/instantclient
ENV ORACLE_HOME /usr/local/instantclient

# Install Oracle instantclient

RUN apk add --no-cache php7-pear php7-dev gcc musl-dev libnsl libaio libc6-compat make --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing/

## Download instantclient
RUN curl -o /tmp/basic.zip https://download.oracle.com/otn_software/linux/instantclient/instantclient-basiclite-linuxx64.zip
RUN curl -o /tmp/sdk.zip https://download.oracle.com/otn_software/linux/instantclient/instantclient-sdk-linuxx64.zip
RUN curl -o /tmp/sqlplus.zip https://download.oracle.com/otn_software/linux/instantclient/instantclient-sqlplus-linuxx64.zip
RUN unzip -d /usr/local/ /tmp/basic.zip
RUN unzip -d /usr/local/ /tmp/sdk.zip
RUN unzip -d /usr/local/ /tmp/sqlplus.zip

RUN ln -s /usr/local/instantclient_* ${ORACLE_HOME}
RUN ln -s ${ORACLE_HOME}/lib* /usr/lib
RUN ln -s ${ORACLE_HOME}/sqlplus /usr/bin/sqlplus
RUN ln -s /lib/libc.so.6 /usr/lib/libresolv.so.2
RUN ln -s /lib64/ld-linux-x86-64.so.2 /usr/lib/ld-linux-x86-64.so.2

## Build OCI8
RUN docker-php-ext-configure oci8 --with-oci8=instantclient,$ORACLE_HOME && docker-php-ext-install oci8
RUN docker-php-ext-enable oci8

#  Clean up
RUN  apk del php7-pear php7-dev gcc musl-dev make &&\
  rm -rf /tmp/*.zip /var/cache/apk/* /tmp/pear/

COPY info.php /var/www/html/info.php