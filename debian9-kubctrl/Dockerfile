FROM gcr.io/google-appengine/debian9:latest

USER root
RUN apt-get update && apt-get install -y apt-transport-https curl gnupg2
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
RUN apt-get update && apt-get install -y kubectl && apt-get clean

# Set common env vars
ENV NODE_ENV production
ENV GCLOUD_TRACE_NEW_CONTEXT=1
ENV NO_UPDATE_NOTIFIER true

