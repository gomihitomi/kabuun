FROM oven/bun:1.1

# デフォの用意されてるやつ。id=1000, group=1000
ARG USERNAME=bun

RUN apt-get update && apt-get install -y \
    git \
    vim \
    lsof \
    curl \
    sudo \
    # xdg-open エラー対策
    xdg-utils \
 && rm -rf /var/lib/apt/lists/*

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

USER $USERNAME
