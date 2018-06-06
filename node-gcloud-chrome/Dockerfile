FROM gcr.io/screencastify-public-registry/node-gcloud:latest

RUN \
  curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable

COPY chrome_launcher.sh /opt/google/chrome/google-chrome
