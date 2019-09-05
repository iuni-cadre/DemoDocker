FROM ubuntu:18.04
WORKDIR /usr/local/bin

# Install dependencies
# RUN apt-get update && apt-get install -y --no-install-recommends build-essential r-base r-cran-randomforest python3.7.3 python3-pip python3-setuptools python3-dev

# Install dependencies
RUN apt-get update && apt-get upgrade -y \
&& apt-get install python3-pip python3-dev \
&& pip3 install --upgrade pip \
&& apt-get install -y r-base

# Define the ENV variables
ENV PYTHONUNBUFFERED=1
COPY requirements.txt .
COPY install.R .

# Install all the python packages required to run the script
RUN pip3 install -r requirements.txt

# Install all the R packages required to run the script
RUN R -e "options(repos = \
  list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2019-04-23/')); \
  install.packages('tidystringdist')" 
RUN R -e "install.packages('checkpoint', dependencies=TRUE)"  
RUN R -e "library('checkpoint')" 
RUN R -e "checkpoint('2019-04-23')"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
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

EXPOSE 80
# ENTRYPOINT ["python", "-u", "__init__.py"]

# RUN R -e "options(repos = \
#  list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2019-04-23/')); \
#  install.packages('tidystringdist')" 
# RUN R -e "install.packages('checkpoint', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"  
# RUN R -e "library('checkpoint')" 
# RUN R -e "checkpoint('2019-04-23')"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
# RUN R -e "install.packages('tidyverse', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                              
# RUN R -e "install.packages('widyr', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                      
# RUN R -e "install.packages('igraph', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                     
# RUN R -e "install.packages('gender', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                     
# RUN R -e "install.packages('genderdata', dependencies=TRUE, repos = 'http://packages.ropensci.org', type = 'source')"                                                                                                          
# RUN R -e "install.packages('gridExtra', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                            
# RUN R -e "install.packages('mgcv', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                                 
# RUN R -e "install.packages('SentimentAnalysis', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                    
# RUN R -e "install.packages('wru', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"
# RUN R -e "install.packages('textcat', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"                                                                                                                    
# RUN R -e "install.packages('vctrs', dependencies=TRUE, repos = 'https://mran.microsoft.com/timemachine')"




 



