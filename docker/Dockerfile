FROM centos:7.4.1708

#install epel
RUN yum install -y -d1 epel-release

#enable Nux repository
RUN rpm -v --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
RUN rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

#enable ffmpeg
RUN yum install -y -d1 ffmpeg ffmpeg-devel
#install sox and other tools
RUN yum install -y -d1 which wget sox curl

#install SCL (software collections)
RUN yum install -y -d1 centos-release-scl
#install python3
RUN yum install -y -d1  rh-python36


#create user mapr
RUN yum install -y -d1 openssl sudo screen
RUN useradd -rm -d /home/mapr -s /bin/bash -G wheel -p "$(openssl passwd -1 mapr)"  mapr
USER mapr
WORKDIR /home/mapr
RUN source scl_source enable rh-python36 && pip3 install --user deepspeech
ENV PATH="/home/mapr/.local/bin:${PATH}"

CMD ["scl", "enable", "rh-python36", "bash"]
