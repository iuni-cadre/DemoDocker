FROM ubuntu:18.04
WORKDIR /usr/local/bin

# This is setting up the correct encoding scheme and locale
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales

RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8 

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
&& apt-get install -y libxml2-dev \
&& apt-get install -y libgit2-dev 

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
COPY WoSmatch/ /usr/local/bin/WoSmatch/

RUN chmod -R 777 /usr/
RUN chmod -R 777 /usr/local/bin/input/
RUN chmod -R 777 /usr/local/bin/scripts/
RUN chmod -R 777 /usr/local/bin/figures/
RUN chmod -R 777 /usr/local/bin/WoSmatch/

# Install all the python packages required to run the script
RUN pip3 install -r requirements.txt

RUN R -e "install.packages('https://cran.r-project.org/src/contrib/Archive/checkpoint/checkpoint_0.4.5.tar.gz')" 

RUN useradd -ms /bin/bash jovyan -g staff
USER jovyan 
WORKDIR /home/jovyan

COPY HelloWorld.R .

RUN mkdir -p /home/jovyan/.checkpoint/${CHECKPOINT_DATE}

RUN R -e  "packageVersion('checkpoint')" && \
    echo "library(checkpoint); checkpoint('${CHECKPOINT_DATE}', scanForPackages = FALSE); .libPaths(); getOption('repos'); setSnapshot('2019-04-23'); .libPaths(); getOption('repos');" >~/.Rprofile && \     
    R -e  "install.packages('tidyverse')" && \                                                                                                                                                                                       
    R -e  "install.packages('widyr')" && \     
    R -e  "install.packages('igraph')" && \                                                                                                                    
    R -e  "install.packages('gender')" && \                                                                                                                   
    R -e  "install.packages('genderdata', repos = 'http://packages.ropensci.org', type = 'source')" && \                                                                                                          
    R -e  "install.packages('gridExtra')" && \                                                                                                                                                                                                                                                                                                                                                                                                                                    
    R -e  "install.packages('mgcv')" && \                                                                                                                              
    R -e  "install.packages('SentimentAnalysis')" && \                                                                                                                    
    R -e  "install.packages('wru')" && \
    R -e  "install.packages('textcat')" && \                                                                                                                   
    R -e  "install.packages('vctrs')" 


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