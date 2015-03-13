FROM ubuntu:14.04

MAINTAINER Barbara Hui <barbara.hui@ucop.edu>

RUN apt-get update && apt-get install -y \
    git \
    libfreetype6 \
    libfreetype6-dev \
    libjpeg-turbo8 \ 
    libjpeg-turbo8-dev \
    liblcms2-2 \
    liblcms2-dev \
    liblcms-utils \
    libtiff5-dev \
    libwebp-dev \
    python-dev \
    python-pip \
    python-setuptools \
    zlib1g-dev 
    
RUN pip install \
    boto \
    configobj \
    mock \
    Pillow \
    requests \
    responses \
    werkzeug

# install Loris
WORKDIR /opt
RUN git clone https://github.com/barbarahui/loris.git
WORKDIR /opt/loris
RUN git checkout ucldc 
RUN useradd -d /var/www/loris -s /sbin/false loris
RUN ./setup.py install

# cache maintenance - need to set up a cron job

# AWS credentials - hack for now
COPY .boto ~/.boto 

EXPOSE 5004

ENTRYPOINT ["python", "/opt/loris/loris/webapp"]
