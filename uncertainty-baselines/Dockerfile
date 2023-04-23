FROM nvidia/cuda:11.8.0-runtime-ubuntu22.04

WORKDIR /home

# python
RUN apt update && apt upgrade
RUN apt install wget build-essential libncursesw5-dev libssl-dev \
libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt install python3.10


# dependencies
# RUN pip install notebook
# RUN pip install scikit-learn
# RUN pip install matplotlib

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y openssh-server

RUN mkdir /var/run/sshd

RUN echo 'root:passwd' | chpasswd

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

EXPOSE 22 8000

CMD ["/usr/sbin/sshd", "-D"]
