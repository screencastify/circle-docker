FROM gcr.io/google-appengine/debian9:latest

# RUN apk add --no-cache libc6-compat
USER root


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
  apt-get -y -t unstable install ffmpeg curl && \
  apt-get -y clean

# install gifski
RUN curl -fsSL "https://gif.ski/gifski-0.9.1.zip" -o /tmp/gifski.zip && \
  unzip /tmp/gifski.zip -d /tmp/gifski && \
  dpkg -i /tmp/gifski/linux/gifski_0.9.1_amd64.deb && \
  rm -rf /tmp/gifski*

# Set common env vars
ENV NODE_ENV production
ENV GCLOUD_TRACE_NEW_CONTEXT=1
ENV NO_UPDATE_NOTIFIER true
