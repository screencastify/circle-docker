FROM gcr.io/screencastify-public-registry/node-gcloud:latest

# install ffmpeg from sid
RUN echo -e "\
  Package: * \n\
  Pin: release a=stable\n\
  Pin-Priority: 900\n\
  \n\
  Package: *\n\
  Pin: release o=Debian\n\
  Pin-Priority: -10\n\
  "
RUN echo "deb http://deb.debian.org/debian unstable main" >> /etc/apt/sources.list && \
    apt-get -y update && \
    apt-get -y -t unstable install ffmpeg && \
    apt-get -y clean

