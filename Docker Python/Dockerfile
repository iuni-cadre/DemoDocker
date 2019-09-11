FROM ubuntu:18.04
WORKDIR /usr/local/bin

# Install dependencies
# RUN apt-get update && apt-get install -y --no-install-recommends build-essential r-base r-cran-randomforest python3.7.3 python3-pip python3-setuptools python3-dev

# Install dependencies
RUN apt-get update && apt-get upgrade -y \
&& apt-get install -y python3 python3-pip

# Define the ENV variables
ENV PYTHONUNBUFFERED=1
COPY requirements.txt .
COPY HelloWorld.py .

# Install all the python packages required to run the script
RUN pip3 install -r requirements.txt

EXPOSE 80
ENTRYPOINT ["python3", "-u", "HelloWorld.py"]



