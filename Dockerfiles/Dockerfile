FROM ubuntu:19.04
WORKDIR /usr/local/bin

# Define the ENV variables
ENV DEBIAN_FRONTEND=noninteractive
ENV CHECKPOINT_DATE 2019-04-23
ENV PKG_CONFIG_PATH=/usr/lib/pkgconfig

# Install the Python Language and it's dependencies
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils \
&& apt-get install -y python3.7 python3-pip

RUN apt-get update && apt-get install -y libssl-dev \
&& apt-get install -y libcurl4-openssl-dev \
&& apt-get install -y libssh2-1-dev \
&& apt-get install -y libxml2-dev

# Install Vim and it's dependencies
RUN apt-get update && apt-get install apt-file -y \
&& apt-file update && apt-get install vim -y

# Install the R Language and it's dependencies
RUN apt-get update && apt-get upgrade -y \
&& apt-get install -y r-base 

# Define the ENV variables
ENV PYTHONUNBUFFERED=1

# Copying all the files in the working directory of the image
COPY requirements.txt .
COPY install.R .
COPY HelloWorld.R .
COPY HelloWorld.py .
COPY Main.java .
COPY Snakefile .
COPY PackageVersions.R .

RUN chmod -R 777 /usr/local/bin/install.R
RUN chmod -R 777 /usr/local/bin/Snakefile
RUN chmod -R 777 /usr/local/bin/PackageVersions.R
RUN chmod -R 777 /usr/local/bin/HelloWorld.R
RUN chmod -R 777 /usr/local/bin/HelloWorld.py
RUN chmod -R 777 /usr/local/bin/Main.java
RUN chmod -R 777 /usr/local/bin/PackageVersions.R

# Copying all the files needed to run the snakemake script in the working directory of the image
COPY input/ /usr/local/bin/input/
COPY scripts/ /usr/local/bin/scripts/
COPY figures/ /usr/local/bin/figures/

RUN chmod -R 777 /usr/
RUN chmod -R 777 /usr/local/bin/input/
RUN chmod -R 777 /usr/local/bin/scripts/
RUN chmod -R 777 /usr/local/bin/figures/

# Install all the python packages required to run the script
RUN pip3 install -r requirements.txt

RUN useradd -ms /bin/bash jovyan -g staff
USER jovyan 
WORKDIR /home/jovyan

# Install all the R packages required to run the script
RUN R -e "install.packages('checkpoint')" && \
    mkdir -p /home/jovyan/.checkpoint/${CHECKPOINT_DATE} && \
    echo "library(checkpoint); checkpoint('${CHECKPOINT_DATE}', scanForPackages = FALSE);" >~/.Rprofile && \                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           
    R -e "install.packages('tidyverse', dependencies=TRUE)" && \                                                                                                              
    R -e "install.packages('widyr', dependencies=TRUE)" && \      
    R -e "install.packages('igraph', dependencies=TRUE)" && \                                                                                                                    
    R -e "install.packages('gender', dependencies=TRUE)" && \                                                                                                                   
    R -e "install.packages('genderdata', dependencies=TRUE, repos = 'http://packages.ropensci.org', type = 'source')" && \                                                                                                          
    R -e "install.packages('gridExtra', dependencies=TRUE)" && \                                                                                                                                                                                                                                                                                                                                                                                                                                    
    R -e "install.packages('mgcv', dependencies=TRUE)" && \                                                                                                                                 
    R -e "install.packages('SentimentAnalysis', dependencies=TRUE)" && \                                                                                                                    
    R -e "install.packages('wru', dependencies=TRUE)" && \
    R -e "install.packages('textcat', dependencies=TRUE)" && \                                                                                                                   
    R -e "install.packages('vctrs', dependencies=TRUE)"

USER root
WORKDIR /usr/local/bin

# Install OpenJDK-8
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean && \
	  rm -rf /var/lib/apt/lists/* && \
  	rm -rf /var/cache/oracle-jdk8-installer;

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f && \
	  rm -rf /var/lib/apt/lists/* && \
	  rm -rf /var/cache/oracle-jdk8-installer;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN javac Main.java

# Make it work under singularity
RUN ldconfig 

EXPOSE 80
# Default command
CMD ["/bin/bash"]