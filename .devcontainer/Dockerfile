# FROM oven/bun:1
FROM node:20-bullseye

# 必要なの入れる
RUN apt-get update && apt-get install -y \
    # git \
    # curl \
    sudo \
    vim \
    lsof \
    # `xdg-open` のエラー対策
    xdg-utils \
 && rm -rf /var/lib/apt/lists/*

# ユーザーを作成
ARG USERNAME=node
# ARG USER_UID=1000
# ARG USER_GID=$USER_UID

# RUN groupadd --gid $USER_GID $USERNAME \
#  && useradd --uid $USER_UID --gid $USER_GID -m -s /bin/bash $USERNAME

RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
 && chmod 0440 /etc/sudoers.d/$USERNAME

# デフォルトシェルをbashにする + プロンプトにgitの情報出す
RUN chsh -s $(which bash) $USERNAME
WORKDIR /usr/share/bash-completion/completions
RUN curl -O https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh \
 && curl -O https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash \
 && chmod a+x git*.*

RUN cat <<EOF >> /home/$USERNAME/.bashrc

source /usr/share/bash-completion/completions/git
source /usr/share/bash-completion/completions/git-prompt.sh
source /usr/share/bash-completion/completions/git-completion.bash

GIT_PS1_SHOWDIRTYSTATE=true
GIT_PS1_SHOWUNTRACKEDFILES=true
GIT_PS1_SHOWUPSTREAM=auto

export PS1="[\\t] \e[1;32m\u\e[m:\e[1;34m\w\e[m \e[1;31m\\\$(__git_ps1 \"(%s)\") \n\e[;m\\$ "
EOF

# bunを入れて、全ユーザが使えるようにする
RUN curl -fsSL https://bun.sh/install | bash
RUN mv /root/.bun/bin/bun /usr/local/bin/
RUN chmod a+x /usr/local/bin/bun

USER $USERNAME
