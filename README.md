# Dockerized Shiny Proxy

Shiny proxy docker image which spins up dockerized shiny apps in a flexdashboard wrapper <br> <br>

1. Build the dockerimage for the example flexdashboard with `docker build -t example_dashboard` . <br>
2. Build the shiny_proxy dockerimage with `docker build -t shiny_proxy` . <br>
This will copy the application.yml and will need the image openanalytics/shinyproxy-demo for including a shiny demo. <br>
3. Run the shiny proxy server with `docker run -d -v /var/run/docker.sock:/var/run/docker.sock --net m-net -p 3838:3838 shiny_proxy` <br>
This will run the server with the two example apps at localhost:3838 with a common shared network m-net. User authentication details can be added in the application.yml.

