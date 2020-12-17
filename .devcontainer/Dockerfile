ARG PYTHON_VERSION=3.9
FROM python:${PYTHON_VERSION}-slim-buster AS development
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN groupadd --gid 1000 nodepy \
    && useradd --uid 1000 --gid nodepy --shell /bin/bash --create-home nodepy
RUN apt-get update && apt-get install -y --no-install-recommends\
    exa \
    curl \
    git \
    vim \
    zsh \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*
RUN curl -LJO https://github.com/sharkdp/bat/releases/download/v0.17.1/bat_0.17.1_amd64.deb \
    && dpkg -i bat_0.17.1_amd64.deb \
    && rm bat_0.17.1_amd64.deb
ARG NODE_VERSION=14
RUN curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y --no-install-recommends\
    nodejs \
    yarn \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*
RUN pip install mkdocs-material
RUN curl -fsSL https://starship.rs/install.sh | bash -s - -y
