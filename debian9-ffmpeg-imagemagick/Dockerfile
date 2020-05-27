FROM gcr.io/google-appengine/debian9:latest

USER root
RUN apt-get update && \
    apt-get install -y ffmpeg imagemagick && \
    apt-get clean

# Set common env vars
ENV NODE_ENV production
ENV GCLOUD_TRACE_NEW_CONTEXT=1
ENV NO_UPDATE_NOTIFIER true
