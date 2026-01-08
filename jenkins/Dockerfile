
FROM jenkins/jenkins:lts-jdk17
USER root
# Install Docker CLI so Jenkins can talk to host Docker via mounted /var/run/docker.sockRUN apt-get update && apt-get install -y ca-certificates curl gnupg lsb-release         && mkdir -p /etc/apt/keyrings         && curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg         && echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release; echo $VERSION_CODENAME) stable" > /etc/apt/sources.list.d/docker.list         && apt-get update && apt-get install -y docker-ce-cli         && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y ca-certificates curl gnupg lsb-release \
    && mkdir -p /usr/share/jenkins/ref/

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

COPY casc.yaml /usr/share/jenkins/ref/casc.yaml

# Cleaned up ENV line - no trailing '>' or missing characters
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
ENV CASC_JENKINS_CONFIG=/usr/share/jenkins/ref/casc.yaml

USER jenkins
