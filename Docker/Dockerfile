# chikai-img

FROM nvidia/cuda:cudnn

MAINTAINER KOZO CHIKAI

WORKDIR /root
ADD Anaconda3-4.2.0-Linux-x86_64.sh /root/
RUN bash Anaconda3-4.2.0-Linux-x86_64.sh -b
ENV PATH /root/anaconda3/bin:$PATH
RUN which python
RUN which pip
RUN pip install chainer 

RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

CMD ["/bin/bash"]