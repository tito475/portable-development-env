FROM linuxserver/code-server:latest

RUN \
  echo "**** install runtime dependencies ****" && \
  curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && \
  apt-get update && \
  apt-get install -y \
    openjdk-17-jdk \
	nodejs \
	maven \
    sudo && \
  npm install -g @angular/cli@15 && \
  echo "**** clean up ****" && \
  apt-get clean && \
  rm -rf \
    /config/* \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*

# ports and volumes
EXPOSE 8443