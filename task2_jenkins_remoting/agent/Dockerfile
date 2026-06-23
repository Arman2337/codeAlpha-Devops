FROM jenkins/inbound-agent:latest

USER root

# Install dependencies required for builds (e.g., Docker client, build tools)
RUN apt-get update && \
    apt-get install -y \
    curl \
    git

# Install Docker CLI so the agent can build docker images
RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-24.0.7.tgz \
  && tar xzvf docker-24.0.7.tgz \
  && mv docker/docker /usr/local/bin \
  && rm -r docker docker-24.0.7.tgz

USER jenkins
