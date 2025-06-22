# codeserver/python/Dockerfile
FROM linuxserver/code-server:latest

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl git build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev libffi-dev liblzma-dev sudo && \
    rm -rf /var/lib/apt/lists/*

ENV PYENV_ROOT=/opt/pyenv
ENV PATH=$PYENV_ROOT/bin:$PYENV_ROOT/shims:$PATH

RUN git clone https://github.com/pyenv/pyenv.git        $PYENV_ROOT && \
    git clone https://github.com/pyenv/pyenv-virtualenv.git \
    $PYENV_ROOT/plugins/pyenv-virtualenv

RUN eval "$(pyenv init --path)" && \
    eval "$(pyenv init -)" && \
    eval "$(pyenv virtualenv-init -)" && \
    pyenv install 3.11.0 && \
    pyenv global 3.11.0 && \
    pip install --upgrade pip

RUN chmod -R a+rwX $PYENV_ROOT

RUN mkdir -p /etc/profile.d && \
    { \
    echo 'export PYENV_ROOT="/opt/pyenv"'; \
    echo 'export PATH="$PYENV_ROOT/bin:$PYENV_ROOT/shims:$PATH"'; \
    echo 'if command -v pyenv >/dev/null 2>&1; then'; \
    echo '  eval "$(pyenv init --path)"'; \
    echo '  eval "$(pyenv init -)"'; \
    echo '  eval "$(pyenv virtualenv-init -)"'; \
    echo 'fi'; \
    } > /etc/profile.d/pyenv.sh && \
    echo 'source /etc/profile.d/pyenv.sh' >> /etc/bash.bashrc

EXPOSE 8443
