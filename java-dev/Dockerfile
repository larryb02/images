FROM rockylinux:9

RUN dnf install -y ncurses \
    man-db \
    git \
    bash-completion


ARG JDK_URL="https://download.java.net/java/GA/jdk25.0.1/2fbf10d8c78e40bd87641c434705079d/8/GPL/openjdk-25.0.1_linux-x64_bin.tar.gz"
ARG JAVA_HOME=/opt/jdk

RUN curl -fsSL "$JDK_URL" -o jdk.tar.gz \
    && mkdir ${JAVA_HOME} \
    && tar xvf jdk.tar.gz -C ${JAVA_HOME} --strip-components=1 \
    && rm jdk.tar.gz

ENV JAVA_HOME=${JAVA_HOME}
ENV PATH=$PATH:"${JAVA_HOME}/bin"

# install Docker
RUN dnf install -y dnf-plugins-core && \
dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo && \
dnf install -y docker-ce-cli

RUN cat << 'EOF' >> ~/.bashrc 
    if [ ! -e /usr/share/bash-competion/completions/git ]; then
            curl -fsSL https://raw.githubusercontent.com/git/git/refs/heads/master/contrib/completion/git-completion.bash -o /usr/share/bash-completion/completions/git
    fi
    curl -fsSL https://raw.githubusercontent.com/git/git/refs/heads/master/contrib/completion/git-prompt.sh -o ~/git-prompt.sh
    source /usr/share/bash-completion/completions/git
    source /usr/share/bash-completion/bash_completion
    source ~/git-prompt.sh
    # Codespaces bash prompt theme 
    # stolen from https://github.com/microsoft/vscode-dev-containers/blob/main/script-library/common-alpine.sh#L217C1-L238C14
    __bash_prompt() {
        local userpart='`export XIT=$? \
            && [ ! -z "${GITHUB_USER}" ] && echo -n "\[\033[0;32m\]@${GITHUB_USER} " || echo -n "\[\033[0;32m\]\u " \
            && [ "$XIT" -ne "0" ] && echo -n "\[\033[1;31m\]➜" || echo -n "\[\033[0m\]➜"`'
        local gitbranch='`\
            if [ "$(git config --get codespaces-theme.hide-status 2>/dev/null)" != 1 ]; then \
                export BRANCH=$(git symbolic-ref --short HEAD 2>/dev/null || git rev-parse --short HEAD 2>/dev/null); \
                if [ "${BRANCH}" != "" ]; then \
                    echo -n "\[\033[0;36m\](\[\033[1;31m\]${BRANCH}" \
                    && if git ls-files --error-unmatch -m --directory --no-empty-directory -o --exclude-standard ":/*" > /dev/null 2>&1; then \
                            echo -n " \[\033[1;33m\]✗"; \
                    fi \
                    && echo -n "\[\033[0;36m\]) "; \
                fi; \
            fi`'
        local lightblue='\[\033[1;34m\]'
        local removecolor='\[\033[0m\]'
        PS1="${userpart} ${lightblue}\w ${gitbranch}${removecolor}\$ "
        unset -f __bash_prompt
    }
    __bash_prompt
EOF

CMD [ "/bin/bash" ]
