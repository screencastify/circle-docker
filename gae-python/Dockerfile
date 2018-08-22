FROM circleci/python:2.7-stretch

USER root
# gcloud
RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip -o google-cloud-sdk.zip && \
      unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true \
  --bash-completion=true --additional-components app alpha beta 
RUN google-cloud-sdk/bin/gcloud config set --installation \
  component_manager/disable_update_check true
ENV PATH "${HOME}/google-cloud-sdk/bin:${PATH}"

RUN gcloud --quiet components install app-engine-python
RUN gcloud --quiet components update app app-engine-python

USER circleci

