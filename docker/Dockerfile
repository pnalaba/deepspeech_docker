FROM centos:7.4.1708

#install epel
RUN yum install -y epel-release

#enable Nux repository
RUN rpm -v --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
RUN rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

#enable ffmpeg
RUN yum install -y ffmpeg ffmpeg-devel
#install sox and other tools
RUN yum install -y which wget sox curl

#install SCL (software collections)
RUN yum install -y centos-release-scl
#install python3
RUN yum install -y rh-python36


#create user mapr
RUN yum install -y openssl sudo screen
RUN useradd -rm -d /home/mapr -s /bin/bash -G wheel -p "$(openssl passwd -1 mapr)"  mapr
USER mapr
WORKDIR /home/mapr
RUN source scl_source enable rh-python36 && pip3 install --user deepspeech
RUN echo '$HOME/.local/bin/deepspeech --model models/output_graph.pbmm --alphabet models/alphabet.txt --lm models/lm.binary --trie models/trie --audio %1 2>/dev/null' > deepspeech/infer.sh

CMD ["scl", "enable", "rh-python36", "bash"]
