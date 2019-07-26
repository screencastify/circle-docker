FROM library/node:10-stretch

ENV HOME /root
WORKDIR $HOME

RUN apt-get update && apt-get install -y unzip build-essential \
      software-properties-common apt-transport-https

# install jq
RUN JQ_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/jq-latest" \
      && curl --silent --show-error --location --fail --retry 3 --output /usr/bin/jq $JQ_URL \
      && chmod +x /usr/bin/jq \
      && jq --version

#docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
 add-apt-repository \
 "deb [arch=amd64] https://download.docker.com/linux/debian \
 $(lsb_release -cs) \
 stable"
RUN apt-get update && apt-get install -y docker-ce


# firebase
# chown hack for https://circleci.com/docs/2.0/high-uid-error/
RUN yarn global add firebase-tools firebase-bolt \
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

