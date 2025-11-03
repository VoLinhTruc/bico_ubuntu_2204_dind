FROM ghcr.io/volinhtruc/bico_ubuntu:22.04_0.0.0

ENV DOCKER_GID=999

# ENV http_proxy=http://$MY_PROXY_IP:$MY_PROXY_PORT
# ENV https_proxy=http://$MY_PROXY_IP:$MY_PROXY_PORT


USER root

# Install Docker CLI ---------------------------------------------
RUN apt-get update && apt install -y ca-certificates curl gnupg lsb-release

# Add Docker's official GPG key
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Set up the Docker repository
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN apt update
RUN apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

RUN apt install -y \
    fuse-overlayfs
# ---------------------------------------------------------------

USER $USERNAME

# Copy and set up entrypoint script
COPY entrypoint.sh /entrypoint.sh
RUN sudo chmod +x /entrypoint.sh

CMD ["/entrypoint.sh", "bash"]
