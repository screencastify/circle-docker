FROM phusion/baseimage:0.11

ENV HOME /root
WORKDIR $HOME

# docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | \
    tee /etc/apt/sources.list.d/yarn.list

# ffmpeg
RUN add-apt-repository ppa:jonathonf/ffmpeg-4 && \
    apt-get update && \
    apt-get install -y ffmpeg && \
    apt-get clean

RUN apt-get update && \
    apt-get install -y \
        libgif-dev git unzip python python-crypto \
        python-psutil python-yaml docker-ce bzip2 expect libgl1-mesa-glx \
        libglu1-mesa yarn build-essential


# nodejs
RUN bash -c "curl -sL https://deb.nodesource.com/setup_12.x | bash -"
RUN apt-get install -y nodejs


RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
    apt-get update && \
    apt-get install -y \
        google-chrome-stable \
        xvfb \
        sudo \
        make

# chown hack for https://circleci.com/docs/2.0/high-uid-error/
RUN sudo npm install --unsafe-perm -g firebase-tools firebase-bolt linklocal \
      lerna && \
      sudo chown root:root -R /usr/lib/node_modules/

# install audiowaveform
RUN add-apt-repository ppa:chris-needham/ppa && \
    apt-get update && \
    apt-get install -y audiowaveform && \
    apt-get clean

RUN useradd -ms /bin/bash ubuntu
RUN echo "ubuntu ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user
ENV DISPLAY :99
USER ubuntu
ENV HOME /home/ubuntu
WORKDIR $HOME


# gcloud
RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip -o google-cloud-sdk.zip && \
      unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true \
  --bash-completion=true --additional-components app alpha beta
RUN google-cloud-sdk/bin/gcloud config set --installation \
  component_manager/disable_update_check true
ENV PATH "${HOME}/google-cloud-sdk/bin:${PATH}"
RUN gcloud components install kubectl

