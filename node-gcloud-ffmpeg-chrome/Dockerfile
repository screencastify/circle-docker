FROM gcr.io/screencastify-public-registry/node-gcloud-chrome:latest

# install gifski
RUN curl -fsSL "https://gif.ski/gifski-0.9.1.zip" -o /tmp/gifski.zip && \
  unzip /tmp/gifski.zip -d /tmp/gifski && \
  dpkg -i /tmp/gifski/linux/gifski_0.9.1_amd64.deb && \
  rm -rf /tmp/gifski*

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
