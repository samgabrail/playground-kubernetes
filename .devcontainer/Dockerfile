FROM mcr.microsoft.com/devcontainers/universal:2-linux
USER root
# Install kubectx, kubens, homebrew, fzf, k9s, and some aliases
RUN git clone https://github.com/ahmetb/kubectx /opt/kubectx \
&& RUN ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx \
&& ln -s /opt/kubectx/kubens /usr/local/bin/kubens \
&& brew install derailed/k9s/k9s \
&& apt-get install fzf -y \
&& alias k="kubectl" \
&& alias kga="kubectl get all" \
&& alias kgn="kubectl get all --all-namespaces" \
&& alias kdel="kubectl delete" \
&& alias kd="kubectl describe" \
&& alias kg="kubectl get" \
&& echo 'alias k="kubectl"' >> /home/codespace/.bashrc \
&& echo 'alias kga="kubectl get all"' >> /home/codespace/.bashrc \
&& echo 'alias kgn="kubectl get all --all-namespaces"' >> /home/codespace/.bashrc \
&& echo 'alias kdel="kubectl delete"' >> /home/codespace/.bashrc \
&& echo 'alias kd="kubectl describe"' >> /home/codespace/.bashrc \
&& echo 'alias kg="kubectl get"' >> /home/codespace/.bashrc


USER codespace
RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" \
&& (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/codespace/.profile \
&& eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

USER root
RUN chown -R $CONTAINER_USER: /home/linuxbrew/.linuxbrew
USER codespace
