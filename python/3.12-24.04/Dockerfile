FROM kubasejdak/base:24.04

# Settings.
ENV UV_INSTALL_DIR=/usr/local/bin
ENV UV_TOOL_BIN_DIR=/usr/local/bin
ENV UV_TOOL_DIR=/usr/local/share/uv/tools

# Install common tools.
RUN sudo apt update && \
    \
    # Install python3 and uv.
    sudo apt install -y python3 python3-pip python3-venv python-is-python3 && \
    sudo -H pip config set global.break-system-packages true && \
    curl -LsSf https://astral.sh/uv/install.sh | sudo env UV_INSTALL_DIR=${UV_INSTALL_DIR} sh && \
    sudo mkdir -p ${UV_TOOL_DIR} && \
    echo "UV_TOOL_DIR=${UV_TOOL_DIR}" | sudo tee -a /etc/environment && \
    echo "UV_TOOL_BIN_DIR=${UV_TOOL_BIN_DIR}" | sudo tee -a /etc/environment && \
    \
    # Install common python tools.
    sudo uv tool install black && \
    sudo uv tool install ruff && \
    \
    # Cleanup image.
    sudo apt autoremove -y && \
    sudo apt clean && \
    sudo rm -rf /var/lib/apt/lists/*
