FROM ubuntu:18.04
WORKDIR /usr/local/bin

# Define the ENV variables
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get upgrade -y \
&& apt-get install -y r-base

COPY install.R .
COPY HelloWorld.R .

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

EXPOSE 80
ENTRYPOINT ["Rscript", "HelloWorld.R"]

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




 
# 3.4.4


