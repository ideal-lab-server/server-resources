# IIT Kanpur IDEAL Lab Server

## Custom Commands

| Command                   | Purpose |
| ------------------------- | ------- |
`userusage`                 | Shows CPU and RAM usage by user. |
`create-venv`               | Creates the default virtual python environment `~/venv/ml-env` and makes the packages installed in the shared environment `/opt/ml` accessible. |
`create-venv custom_name`   | Creates the custom virtual python environment `~/venv/custom_name` and makes the packages installed in the shared environemnt `/opt/ml` accessible.|
`activate-venv`             | Activates the default virtual python environment `~/venv/ml-env`, if it exists. |
`activate-venv custom_name` | Activates the custom virtual python environment `~/venv/custom_name`, if it exists. |
`jupyterlab` | Launches JupyterLab using the shared environment.

---
## IMPORTANT

These commands are installed system-wide and are available to all users. To modify any of these commands, make
a request to the administrator to update the `/etc/bash.bashrc` file.