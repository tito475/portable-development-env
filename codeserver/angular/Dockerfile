FROM linuxserver/code-server:latest

RUN \
  echo "**** install runtime dependencies ****" && \
  curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && \
  apt-get update && \
  apt-get install -y \
	nodejs \
	wget \
	gnupg \
	ca-certificates \
    sudo && \
  npm install -g @angular/cli@15 && \
  wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list && \
  apt-get update && apt-get install -y google-chrome-stable && \
  echo "**** clean up ****" && \
  apt-get clean && \
  rm -rf \
    /config/* \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*

# ports and volumes
EXPOSE 8443