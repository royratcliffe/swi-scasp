FROM mcr.microsoft.com/devcontainers/base:alpine-3.20

# Install the latest version of SWI-Prolog from the Alpine Linux edge repository.
# This is necessary to get the latest version of SWI-Prolog, which is required for some Prolog packs.
# The --repository option specifies the repository to use for the installation.
# https://pkgs.alpinelinux.org/packages?name=swi-prolog&branch=edge
RUN sudo apk add swi-prolog --repository=https://dl-cdn.alpinelinux.org/alpine/edge/testing --repository=https://dl-cdn.alpinelinux.org/alpine/edge/main

# Install essential build tools. Need for Prolog packs with foreign libraries.
RUN sudo apk add build-base

# Install the s(SCASP) Skolemised Constraint Answer Set Programming
# package. It needs a prefix override in order to symbolically link the
# `scasp` binary link.
#
# Assume that the container has a `PATH` element at `.local/bin` relative
# to `HOME` already configured. This is true for Alpine containers.
# Install binaries to this directory in order to obviate permission
# problems.
#
# Take care when running as `sudo`. It changes the home directory.
# Set the Docker user and their working directory before making the local binary
# directory before installing s(CASP).
USER vscode
WORKDIR /home/vscode
RUN mkdir -p $HOME/.local/bin && SWIPL_PREFIX=$HOME/.local swipl pack install -y scasp
