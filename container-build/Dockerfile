# Use the httpd-parent image as base
FROM quay.io/redhattraining/httpd-parent

# Overrides the EXPOSE instruction from the parent image and changes the port to 8080
EXPOSE 8080

# Indicates the changed port that the web server runs on:
LABEL io.k8s.description="A basic Apache HTTP Server child image, uses ONBUILD" \
      io.k8s.display-name="Apache HTTP Server" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="apache, httpd"

# Run the web server on an unprivileged port (that is, greater than 1024)
RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf

# Change the group ID and permissions of the folders where the web server process reads and writes files
RUN chgrp -R 0 /var/log/httpd /var/run/httpd && \
    chmod -R g=u /var/log/httpd /var/run/httpd

USER 1001