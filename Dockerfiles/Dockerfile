FROM ubuntu:18.04
WORKDIR /usr/local/bin

# Define the ENV variables
ENV DEBIAN_FRONTEND=noninteractive

# Install the Python Language and it's dependencies
RUN apt-get update && apt-get upgrade -y \
&& apt-get install -y python3 python3-pip

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

# Install all the python packages required to run the script
RUN pip3 install -r requirements.txt

# Install all the R packages required to run the script
RUN R -e "options(repos = \
  list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2019-04-23/')); \
      install.packages('tidystringdist')" 
RUN R -e "install.packages('checkpoint', dependencies=TRUE)"  
RUN R -e "library('checkpoint')" 
# RUN R -e "checkpoint('2019-04-23')"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
RUN R -e "install.packages('tidyverse', dependencies=TRUE)"                                                                                                              
RUN R -e "install.packages('widyr', dependencies=TRUE)"                                                                                                                      
RUN R -e "install.packages('igraph', dependencies=TRUE)"                                                                                                                     
RUN R -e "install.packages('gender', dependencies=TRUE)"                                                                                                                     
RUN R -e "install.packages('genderdata', dependencies=TRUE, repos = 'http://packages.ropensci.org', type = 'source')"                                                                                                          
RUN R -e "install.packages('gridExtra', dependencies=TRUE)"                                                                                                                            
RUN R -e "install.packages('mgcv', dependencies=TRUE)"                                                                                                                                 
RUN R -e "install.packages('SentimentAnalysis', dependencies=TRUE)"                                                                                                                    
RUN R -e "install.packages('wru', dependencies=TRUE)"
RUN R -e "install.packages('textcat', dependencies=TRUE)"                                                                                                                    
RUN R -e "install.packages('vctrs', dependencies=TRUE)"

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
ENTRYPOINT ["python3", "-u", "HelloWorld.py"]



































 



