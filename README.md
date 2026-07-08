# Configuring GitHub Codespaces with devcontainer.json

This document outlines the procedure for configuring a GitHub Codespaces environment using a `.devcontainer/devcontainer.json` file.

## Purpose and Benefits

Configuring a Codespace establishes a reproducible, containerized local development environment. This approach provides several advantages:
- **Reproducibility**: Ensures all developers use identical, pre-configured environments.
- **Host Isolation**: Prevents cluttering the host machine with project-specific dependencies, libraries, and tools.
- **Rapid Provisioning**: Allows new environments to be instantiated directly from the repository without manual setup.

## Configuration Details

The environment is defined by a file located at `.devcontainer/devcontainer.json` within the repository root. This file specifies the container image, additional features, VS Code customizations, and initialization scripts.

### Example `devcontainer.json`

The following JSON block provides a base configuration for a Python 3.13 environment running on Debian Bullseye. It includes Node.js LTS, configures VS Code with standard extensions, and installs the `uv` package installer upon creation.

```json
{
  "name": "Python 3.13",
  "image": "mcr.microsoft.com/devcontainers/python:3.13-bullseye",
  "features": {
    "ghcr.io/devcontainers/features/node:1": {
      "version": "latest"
    }
  },
  "customizations": {
    "vscode": {
      "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python",
        "python.linting.enabled": true
      },
      "extensions": [
        "ms-python.python",
        "ms-python.vscode-pylance",
        "ms-python.vscode-python-envs",
        "GitHub.copilot"
      ]
    }
  },
  "postCreateCommand": "pip install uv"
}
```

### Launching the Codespace

Once the `.devcontainer/devcontainer.json` file is committed to the repository, you can launch the Codespace. To facilitate quick creation and resumption, construct a URL using the following format:

`https://codespaces.new/[OWNER]/[REPO]?quickstart=1`

The `?quickstart=1` parameter prompts the system to resume an existing Codespace for the repository if one is already running, rather than starting a new instance.

---

**Reference:**
Willison, S. [Configuring GitHub Codespaces using devcontainers](https://til.simonwillison.net/github/codespaces-devcontainers).
