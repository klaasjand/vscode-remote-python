FROM python:3.12-slim-bookworm
LABEL maintainer="Klaas Jan Dijksterhuis"

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create a user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        curl \
        git

COPY .devcontainer/requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt \
    && rm -f /tmp/requirements.txt

# Remove or comment out to use root user
ENV PATH=${PATH}:/home/$USERNAME/.local/bin
USER $USERNAME
