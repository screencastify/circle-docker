FROM phusion/baseimage

ENV HOME /root
WORKDIR $HOME

# docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
 add-apt-repository \
 "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
 $(lsb_release -cs) \
 stable"

RUN apt-get update
RUN apt-get install -y libgif-dev ffmpeg git unzip python python-crypto \
      python-psutil python-yaml docker-ce

# nodejs
RUN bash -c "curl -sL https://deb.nodesource.com/setup_7.x | bash -"
RUN apt-get install -y nodejs 


# gcloud
RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip -o google-cloud-sdk.zip && \
      unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true \
  --bash-completion=true --additional-components app alpha beta 
RUN google-cloud-sdk/bin/gcloud config set --installation \
  component_manager/disable_update_check true
ENV PATH "${HOME}/google-cloud-sdk/bin:${PATH}"
RUN gcloud components install kubectl

RUN \
  curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable xvfb sudo make

COPY chrome_launcher.sh /opt/google/chrome/google-chrome
RUN npm install -g firebase-tools firebase-bolt


# blender
RUN mkdir -p /opt/blender && \
      curl -SL \
      http://ftp.nluug.nl/pub/graphics/blender/release/Blender2.78/blender-2.78a-linux-glibc211-x86_64.tar.bz2 \
 | tar -xjC /opt/blender --strip-components=1

RUN useradd -ms /bin/bash ubuntu
RUN echo "ubuntu ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user
ENV DISPLAY :99
USER ubuntu
ENV HOME /home/ubuntu
WORKDIR $HOME

