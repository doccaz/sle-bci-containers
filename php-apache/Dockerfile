FROM registry.suse.com/bci/php-apache:8
ENV my_dependencies="wget java-1_8_0-openjdk php8-pecl php8-gd php8-intl glibc-locale-base unixODBC-devel unzip php8-devel gawk make  msodbcsql18 mssql-tools"
RUN set -eux; \
	zypper -n in SUSEConnect; \
	suseconnect -r *******; \
	suseconnect -p sle-module-legacy/15.6/x86_64; \
	zypper ar https://packages.microsoft.com/sles/15/prod/ microsoft; \
	zypper --gpg-auto-import-keys refresh; \
	ACCEPT_EULA=y zypper -n in -y $my_dependencies; 
    
# additional setup steps
RUN wget https://getcomposer.org/download/latest-stable/composer.phar -O /bin/composer

RUN zypper -n --no-gpg-checks install -y \
	https://download.oracle.com/otn_software/linux/instantclient/2112000/el9/oracle-instantclient-basic-21.12.0.0.0-1.el9.x86_64.rpm \
	https://download.oracle.com/otn_software/linux/instantclient/2112000/el9/oracle-instantclient-devel-21.12.0.0.0-1.el9.x86_64.rpm
 

RUN pecl install oci8 mongodb redis sqlsrv pdo_sqlsrv
RUN echo "extension=oci8.so" > /etc/php8/conf.d/oci.ini \
    && echo "/usr/lib/oracle/21/client64/lib" > /etc/ld.so.conf.d/oracle.conf \
    && echo "extension=oci8.so" >> /etc/php8/apache2/php.ini \
    && echo "extension=mongodb.so" >> /etc/php8/conf.d/mongodb.ini \
    && echo "extension=redis.so" >> /etc/php8/conf.d/redis.ini \
    && echo "extension=sqlsrv.so" >> /etc/php8/conf.d/sqlsrv.ini \
    && echo "extension=pdo_sqlsrv.so" >> /etc/php8/conf.d/pdo_sqlsrv.ini \
    && echo "catch_workers_output = yes" >> /etc/php8/apache2/php.ini \
    && echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc \
    && source ~/.bashrc \
    && echo "AnsiNPW=1" > /etc/unixODBC/odbc.ini \
    && ln -s /etc/unixODBC/odbc.ini /etc/odbc.ini \
    && ln -s /etc/unixODBC/odbcinst.ini /etc/odbcinst.ini \
    && ln -s /etc/unixODBC/ODBCDataSources /etc/ODBCDataSources

# Copy the app into the Apache2 document root
COPY app/ .

