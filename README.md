This project is described in detail in the corresponding blog post series:

**Part I:** https://medium.com/analytics-vidhya/shiny-dashboards-with-flexdashboard-e66aaafac1f2 <p>

**Part II:** https://medium.com/analytics-vidhya/deploying-a-shiny-flexdashboard-with-docker-cca338a10d12

# Dockerized Shiny Proxy Server

Shiny proxy docker image which spins up dockerized Shiny apps in a Flexdashboard HTML wrapper. <br> <br>

1. Build the dockerimage for the example flexdashboard with `docker build -t example_dashboard .` in directory of corresponding Dockerfile. <br>
2. Pull the image for the shiny demo app via `docker pull openanalytics/shinyproxy-demo` <br>
3. Build the shiny_proxy dockerimage with `docker build -t shiny_proxy .` in directory of corresponding Dockerfile. <br>
This will copy the application.yml and will need the image openanalytics/shinyproxy-demo for including a shiny demo. <br>
4. Run the shiny proxy server with `docker run -d -v /var/run/docker.sock:/var/run/docker.sock --net m-net -p 3838:3838 shiny_proxy`. This maps a local volume to a directory in the docker container and maps the docker container port 3838 to your port 3838. This will run the shiny proxy server with the two example apps at localhost:3838 with a common shared container network m-net. User authentication details can be added in the application.yml.

## Page links
[Static HTML Flexdashboard](https://timosch29.github.io/Dockerized-Shiny-Proxy-Server/example_dashboard/dashboard_example) <br>
[Same Flexdashboard with Shiny reactivity](https://timosch.shinyapps.io/dashboard_example/#section-test-plotly-and-shiny-elements)
