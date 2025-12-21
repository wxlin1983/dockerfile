# 1. Use the Microsoft-optimized Node.js image
FROM mcr.microsoft.com/devcontainers/javascript-node:0-22

# 2. Update system packages to latest
USER root
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    htop \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# 3. Prepare directories and permissions
# We create the workspace folder and ensure 'node' owns it
USER root
RUN mkdir -p /workspaces && \
    chown -R node:node /workspaces

# 4. Switch to the non-root user provided by the base image
USER node
WORKDIR /workspaces
