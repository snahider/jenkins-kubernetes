FROM jenkinsci/ssh-slave

# Install Docker client
ENV DOCKER_BUCKET get.docker.com
ENV DOCKER_VERSION 17.04.0-ce
ENV DOCKER_SHA256 c52cff62c4368a978b52e3d03819054d87bcd00d15514934ce2e0e09b99dd100

RUN set -x \
&& curl -fSL "https://${DOCKER_BUCKET}/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz" -o docker.tgz \
&& echo "${DOCKER_SHA256} *docker.tgz" | sha256sum -c - \
&& tar -xzvf docker.tgz \
&& mv docker/* /usr/local/bin/ \
&& rmdir docker \
&& rm docker.tgz \
&& docker -v

# Install K8S client
RUN curl -L https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl -o kubectl \
&& chmod +x kubectl \
&& mv kubectl /usr/local/bin/kubectl

# Grant jenkins access to docker socket
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint

ENTRYPOINT ["docker-entrypoint"]