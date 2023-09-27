# This is not fully compatible builder Dockerfile, but meets the needs of tests
FROM quay.io/centos/centos:stream9
RUN dnf install -y python3-pip
RUN python3 -m pip install ansible-core ansible-runner
RUN mkdir -p /runner/{env,inventory,project,artifacts} /home/runner/.ansible/tmp
RUN chmod -R 777 /runner /home/runner
WORKDIR /runner
ENV HOME=/home/runner
## Container stops after run with this command
# CMD ["ansible-runner", "run", "/runner"]
