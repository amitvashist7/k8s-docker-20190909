# Base Image
FROM ubuntu:16.04 

# Owner
MAINTAINER Amit <amitvashist7@gmail.com>

# Update the Apt-Repo
RUN apt-get update 

# Install Apache
RUN apt-get install apache2 -y 

# Expose on port 80
EXPOSE 80 8080

# Create info file
COPY amit.txtx  /var/www/html/info.html

# Start Apache Service
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
