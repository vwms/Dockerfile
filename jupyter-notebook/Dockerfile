FROM ubuntu:16.04

MAINTAINER zhoujunqian <zjqzero@gmail.com>

ADD start.sh /start.sh
ADD requirements2.txt /requirements2.txt
ADD requirements3.txt /requirements3.txt
COPY ta-lib-0.4.0-src.tar.gz ta-lib.tar.gz

RUN apt-get update
RUN apt-get install -y python python3 python-dev python3-dev python-pip python3-pip
RUN pip3 install --no-cache-dir jupyter ipython
RUN python2 -m pip install --no-cache-dir ipykernel
RUN python2 -m ipykernel install --user

RUN tar -zxvf ta-lib.tar.gz
RUN rm -rf ta-lib.tar.gz 
WORKDIR /ta-lib 
RUN ./configure --prefix=/usr
RUN make
RUN make install
RUN cd ..
RUN rm -rf ta-lib

WORKDIR /
RUN pip install --no-cache-dir -r requirements2.txt
# RUN pip3 install -r requirements3.txt

RUN rm -rf /var/lib/apt/lists/*

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888



CMD ["/start.sh"]
