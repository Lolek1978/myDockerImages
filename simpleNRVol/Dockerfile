

FROM centos:centos7


MAINTAINER Paweł Mazurek <lolo78@o2.pl>

RUN yum install -y --setopt=tsflags=nodocs httpd.x86_64 && yum clean all -y

# A custom httpd.conf that
# 1. binds to port 8080
# 2. sends all logs to stdout through log = "|more"
COPY conf/httpd.conf /etc/httpd/conf/httpd.conf

# Copy over an index.html to the default location and then make it a volume
# The permission changes actually appears due to a bug with Windows and Mac. It looks like
# we could have just "ls" on the directory to get the chmod to stick
VOLUME ["/var/www/html"]
RUN ls -la /var/www/html/ && chmod -R a+rwx /var/www/html/


#Expose the port
EXPOSE 8080

# need to change some permissions to allow non-root user to start things
# had to do these steps to give the httpd deamon the ability to.
# This actually appears due to a bug with Windows and Mac. It looks like
# we could have just "ls" on the directory to get the chmod to stick
RUN rm -rf /run/httpd && mkdir /run/httpd && chmod -R a+rwx /run/httpd

USER 1001


CMD /usr/sbin/apachectl -DFOREGROUND

#run it with
 #docker run -p 80:80 6e3c25bdca9b
