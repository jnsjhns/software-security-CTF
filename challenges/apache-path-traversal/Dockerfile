FROM httpd:2.4.49

COPY apache/httpd.conf /usr/local/apache2/conf/httpd.conf
COPY web/ /usr/local/apache2/htdocs/

# Flag liegt außerhalb des DocumentRoot
COPY flag/flag.txt /flag/flag.txt
RUN chmod 644 /flag/flag.txt

EXPOSE 80