FROM library/node:8.9-stretch


RUN apt-get update && apt-get install -y unzip
# firebase
# chown hack for https://circleci.com/docs/2.0/high-uid-error/
RUN npm install --unsafe-perm -g firebase-tools firebase-bolt linklocal \
      lerna && \
      chown root:root -R /usr/local/lib/node_modules/

# gcloud
RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip -o google-cloud-sdk.zip && \
      unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --usage-reporting=true --path-update=true \
  --bash-completion=true --additional-components app alpha beta 
RUN google-cloud-sdk/bin/gcloud config set --installation \
  component_manager/disable_update_check true
ENV PATH "${HOME}/google-cloud-sdk/bin:${PATH}"
RUN gcloud components install kubectl

