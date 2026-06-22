# hadolint ignore=DL3007
FROM dast1986/slough-dev-dc-generic-base:1.0.1 AS base

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install `uv`
RUN echo "# Autocompletion for UV" >> .bashrc.local && \
    /home/developer/.local/bin/uv generate-shell-completion bash >> .bashrc.local && \
    echo >> .bashrc.local

# Configure `uv`
ENV UV_PYTHON_PREFERENCE=only-managed

# Install the Ansible tools
RUN /home/developer/.local/bin/uv self update && \
    /home/developer/.local/bin/uv tool install ansible-core && \
    /home/developer/.local/bin/uv tool install ansible-lint

# Configure Starship
ENV PROMPTNAME="ANSIBLE"

# Add update scripts
COPY ./update/ /opt/update-dc/

# Update the system
# hadolint ignore=DL3004
RUN sudo /opt/update-dc/000-update-dev-dc.sh

# Set the default command to bash
CMD ["bash"]