# image for running DeepFigures

FROM tensorflow/tensorflow:latest-py3

ENV LC_ALL C.UTF-8
ENV TZ=Asia/Kolkata \
    DEBIAN_FRONTEND=noninteractive
# install system packages

RUN apt update
RUN apt upgrade -y
RUN apt install software-properties-common -y
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
RUN add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
RUN dpkg --purge --force-depends ca-certificates-java
RUN apt-get clean \
 && apt-get update --fix-missing \
 && apt-get install -y \
    git \
    ca-certificates-java \
    curl \
    gcc \
    build-essential \
    tcl \
    g++ \
    zlib1g-dev \
    libjpeg8-dev \
    libtiff5-dev \
    libjasper-dev \
    libpng-dev \
    tcl-dev \
    tk-dev \
    python3 \
    python3-pip \
    python3-tk \
    ghostscript \
    openjdk-8-jre 
RUN apt-get install -y \
    poppler-utils \
    texlive-latex-base \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    texlive-latex-extra
WORKDIR /work

# install python packages

ADD ./requirements.txt /work

RUN pip3 install --upgrade pip setuptools wheel \
 && pip install Cython==0.25.2
RUN pip3 install -r ./requirements.txt

ADD ./vendor/tensorboxresnet /work/vendor/tensorboxresnet
RUN pip3 install -e /work/vendor/tensorboxresnet

ADD . /work
RUN pip3 install --quiet -e /work

CMD [ "/bin/bash" ]
