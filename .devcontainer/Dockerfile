FROM rubensa/ubuntu-tini-dev:20.04 as base
# Architecture component of TARGETPLATFORM (platform of the build result)
ARG TARGETARCH
# Configure apt and install mysql-client and unixodbc-dev
RUN echo "# Installing mysql-client, unixodbc and unixodbc-dev..." \
  && sudo apt-get update; sudo DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-client unixodbc unixodbc-dev
# In ARM64 install python2 (needed to re-build node-sass) and phantomjs (as there is no pre-binary build for ruby gem)
RUN if [ "$TARGETARCH" = "arm64" ]; then echo "# Installing python2 and phantomjs..." && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install python2 phantomjs; fi
# Clean up apt
RUN sudo apt-get autoremove -y \
  && sudo apt-get clean -y \
  && sudo rm -rf /var/lib/apt/lists/*

FROM base

# Keep container running (for use in VSCode)
CMD [ "tail", "-f", "/dev/null" ]
