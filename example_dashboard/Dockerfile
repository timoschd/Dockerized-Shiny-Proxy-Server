FROM r-base:latest

MAINTAINER Tim M.Schendzielorz "tim.schendzielorz@googlemail.com"
 
# Install dependencies and Download and install shiny server
# not all libs necessary
RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    libssl-dev \
	libudunits2-dev \
	libv8-dev \
	libmariadb-dev \
	libmariadb-dev-compat \
	default-libmysqlclient-dev \
	unixodbc-dev \
	libsqlite3-dev \
	libgdal-dev \
	libxml2-dev \
	libxt-dev && \
    wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.12.933-amd64.deb -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.12.933-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    R -e "install.packages(c('shiny', 'flexdashboard', 'dplyr','knitr','d3heatmap'),dependencies = TRUE)" && \
    R -e 'if(!require(devtools)) { install.packages("devtools") }; library(devtools);' && \
    R -e "library(devtools); install_cran('plotly')" && \
	R -e "library(devtools); install_cran('RMySQL')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    rm -rf /var/lib/apt/lists/*



	
RUN mkdir -p /bin
COPY dashboard_example.Rmd    /bin/dashboard_example.Rmd

# make all app files readable (solves issue when dev in Windows, but building in Ubuntu)
RUN chmod -R 755 /bin

EXPOSE 3838

CMD ["R", "-e", "rmarkdown::run('/bin/dashboard_example.Rmd', shiny_args = list(port = 3838, host = '0.0.0.0'))"]
