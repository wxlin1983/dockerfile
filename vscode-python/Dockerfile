# 1. Use the Microsoft-optimized Python 3.14 (Trixie) image
FROM mcr.microsoft.com/devcontainers/python:3.14-trixie

# 2. Update system packages to latest
USER root
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    htop \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# 3. Install uv using the official binary
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 4. Setup environment variables
# UV_LINK_MODE=copy is essential for stability on Mac/Docker volume mounts
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    UV_LINK_MODE=copy \
    UV_PYTHON_PREFERENCE=managed \
    UV_CACHE_DIR=/home/vscode/.cache/uv

# 5. Prepare directories and permissions
# We create the cache and workspace folders and ensure 'vscode' owns them
USER root
RUN mkdir -p /home/vscode/.cache/uv /workspaces && \
    chown -R vscode:vscode /home/vscode/.cache/uv /workspaces

# 6. Switch to the non-root user provided by the base image
USER vscode
WORKDIR /workspaces

# 7. Pre-install Python 3.14 via uv
# This ensures the runtime is ready before you even open the terminal
RUN uv python install 3.14