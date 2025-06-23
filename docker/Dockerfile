## Base image with python3 installed
FROM python:3.10.2-alpine3.14


## Copy all files into the docker image
COPY . /myapp 


## Change the default directory to myip
WORKDIR /myapp


## Install the requirements 
RUN python -m pip install -r requirements.txt


CMD ["/bin/sh", "-c", "python /myapp/app.py"]