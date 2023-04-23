FROM pytorch/pytorch:1.12.1-cuda11.3-cudnn8-devel

WORKDIR /home

# python
# opencv dependency
RUN apt-get update
RUN apt-get -y install libgl1-mesa-glx
RUN apt-get -y install libsm6
RUN apt-get -y install libxrender-dev
RUN apt-get -y install libxext6
# pip install 
RUN pip install opencv-python

# dependencies
RUN pip install notebook
RUN pip install scikit-learn
RUN pip install matplotlib

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y openssh-server

RUN mkdir /var/run/sshd

RUN echo 'root:passwd' | chpasswd

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

EXPOSE 22 8000

CMD ["/usr/sbin/sshd", "-D"]
