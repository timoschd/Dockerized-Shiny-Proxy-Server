FROM r-base:latest
#FROM rocker/shiny-verse:latest 

MAINTAINER Tim M.Schendzielorz "tim.schendzielorz@googlemail.com"
 



# Install dependencies and Download and install shiny server
RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    libssl-dev \
	libxml2-dev \
    libxt-dev && \
    wget --no-verbose https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    R -e "install.packages(c('shiny', 'flexdashboard', 'dplyr','knitr','d3heatmap'))" && \
    R -e 'if(!require(devtools)) { install.packages("devtools") }; library(devtools);' && \
    R -e "library(devtools); install_cran('plotly')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    rm -rf /var/lib/apt/lists/*

# Install dependencies 
#RUN  echo 'install.packages(c("knitr","flexdashboard", "d3heatmap"), \
 #       repos="http://cran.us.r-project.org", \
 #       dependencies=TRUE)' > /tmp/packages.R \
  #      && Rscript /tmp/packages.R
	
	
RUN mkdir -p /bin
COPY dashboard_example.Rmd    /bin/dashboard_example.Rmd

# make all app files readable (solves issue when dev in Windows, but building in Ubuntu)
RUN chmod -R 755 /bin

EXPOSE 3838

CMD ["R", "-e", "rmarkdown::run('/bin/dashboard_example.Rmd', shiny_args = list(port = 3838, host = '0.0.0.0'))"]