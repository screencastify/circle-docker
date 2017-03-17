FROM phusion/baseimage

RUN OLDDIR=`pwd`
WORKDIR $HOME

# gcloud
RUN wget https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip && \
      unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true \
  --bash-completion=true --additional-components app alpha beta 
RUN google-cloud-sdk/bin/gcloud config set --installation \
  component_manager/disable_update_check true
ENV PATH "${HOME}/google-cloud-sdk/bin:${PATH}"
WORKDIR $OLDDIR

RUN apt-get update
RUN apt-get install -y libgif-dev ffmpeg git

