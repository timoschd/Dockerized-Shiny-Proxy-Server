FROM openjdk:8-jre

# install shiny proxy server
RUN wget https://www.shinyproxy.io/downloads/shinyproxy-2.3.0.jar -O /opt/shinyproxy/shinyproxy.jar

# make directory and copy the application.yml file into it
RUN mkdir -p /opt/shinyproxy/

COPY application.yml /opt/shinyproxy/application.yml

# make all app files readable (solves issue when dev in Windows, but building in Ubuntu)
RUN chmod -R 755 /opt/shinyproxy/

CMD ["java", "-jar", "/opt/shinyproxy/shinyproxy.jar"]