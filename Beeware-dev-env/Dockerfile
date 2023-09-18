FROM python:3.11-slim

ARG USERNAME=walid
ARG USER_UID=1000
ARG GROUP_UID=1000

# Create the user
RUN groupadd --gid $GROUP_UID $USERNAME \
    && useradd --uid $USER_UID --gid $GROUP_UID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt update -y \
    && apt upgrade -y \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME

#RUN sudo apt update && sudo apt upgrade -y

RUN sudo apt install --no-install-recommends build-essential git pkg-config python3-dev python3-venv libgirepository1.0-dev libcairo2-dev gir1.2-webkit2-4.0 libcanberra-gtk3-module -y \
    && sudo apt-get autoremove -y \
    && sudo rm -rf /tmp/* \
    && sudo rm -rf /var/lib/apt/lists/* \
    && sudo apt-get clean \
    && python3.11 -m pip install briefcase --no-cache-dir

CMD ["/bin/bash"]

