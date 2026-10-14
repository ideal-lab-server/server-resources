# IIT Kanpur IDEAL Lab Server

## Python Virtual Environment - Quick Start

This server provides a SHARED Python virtual environment for commonly used
packages. Each user can also create PRIVATE environments for additional
packages.

---
### 1. Shared Environment
---

Location:
    
```
/opt/ml
```
    
This is an administrator-created Python 3.12 virtual environment. It contains commonly used packages such as:

```
NumPy                  SciPy
pandas                 Matplotlib
scikit-learn           PyTorch + CUDA
Gymnasium              Stable-Baselines3
JupyterLab             TensorBoard
```

The shared environment is managed by the administrator. NEVER modify, upgrade, or install packages in `/opt/ml` yourself.

---
### 2. Your Private Environment
---

Your private environments are stored under:

```
~/venv/
```

A private environment can access packages installed in `/opt/ml` and can
also contain additional packages installed by you. Private packages do not modify the shared environment.


---
### 3. Creating a Private Environment
---

The administrator has provided a system-wide custom command:

```
create-venv
```

This creates the default private environment `~/venv/ml-venv`. If the parent directory `~/venv` does not exist, the command `create-venv` will create it. The user need not manually create it. For creating a custom environment `~/venv/custom_name`, use the following command.

```
create-venv custom_name
```

---
### 4. Activating a Private Environment
---

The administrator has also provided:

```
activate-venv
```
    
This activates the default environment `~/venv/ml-venv`. For a custom environment, use:

```
activate-venv custom_name
```

This activates `~/venv/custom_name`. If the requested environment does not exist, the command will report that the environment cannot be found.


After activation, verify the Python being used:
```
which python
```
It should point to something similar to
`/home/username/venv/ml-venv/bin/python`.

---
### 5. Shared Packages and Private Packages
---

Your private environment is configured to access the shared packages in `/opt/ml/lib/python3.12/site-packages/`. If the same package exists in both the shared and private environments, Python will normally use the private copy. To check where a package is being loaded from, run the following command after activating a virtual environment.

```
python -c "import PACKAGE_NAME; print(PACKAGE_NAME.__file__)"
```

For example, the following command will show where the package `torch` is loaded from.
```
python -c "import torch; print(torch.__file__)"
```

A shared package will normally show a path containing:
`/opt/ml/`. A private package will normally show a path containing:
`/home/username/venv/`.


---
### 6. Installing Additional Packages
---

First activate your private environment, and then install packages using:
```
python -m pip install PACKAGE_NAME
```

For a specific version:
```
python -m pip install PACKAGE_NAME==VERSION
```

Example:
```
python -m pip install rich
python -m pip install numpy==2.5.3
```

To see the packages installed in the shared environment, run:
```
/opt/ml/bin/python -m pip list
```

---
### 7. Every Time You Login
---

Your virtual environment is not automatically activated in a new terminal. Activate it with:
```
activate-venv
```

For a custom environment:
```
activate-venv custom_name
```

You can then run your programs normally:
```
python your_script.py
```
When finished:
```
deactivate
```

Note that `deactivate` does NOT delete your environment.


---
### 8. Important Rules
---

- Use shared packages whenever they meet your requirements.

- Install additional packages only in your private environment.

- NEVER use sudo to install packages in your private environment.

- NEVER modify `/opt/ml` yourself.

- Avoid unnecessarily reinstalling packages already available in the shared environment.

- If a package is useful to many researchers, ask the administrator to consider adding it to `/opt/ml`.

- Be careful when installing different versions of major packages such as `NumPy`, `SciPy`, `PyTorch`, `pandas`, or `scikit-learn`, as this may create dependency conflicts.


---
### 9. Important Locations
---

| Directory                               | Contents                    |
| --------------------------------------- | --------------------------- |
| `\opt\ml`                               | Shared Virtual Environments |
| `/opt/ml/bin/python`                    | Shared Python               |
| `/opt/ml/lib/python3.12/site-packages/` | Shared Packages             |
| `~/venv/`                               | Private Environments        |
| `~/venv/ml-venv`                        | Default Private Environment |

---
### 10. Important Commands
---

| Command | Purpose |
| ------- | ------- |
| `create-venv` | Create the default environment. |
| `create-venv custom_name` | Create a named environment. |
| `activate-venv` | Activate the default environment, if it exists. |
| `activate-venv custom_name` | Activate the named environment, if it exists. |
| `which python` | Check Python |
| `python -m pip install PACKAGE_NAME` | Install a package inside a private environment. |
| `python -m pip install PACKAGE_NAME==VERSION` | Install a specific version of the package inside a private environment. |
| `python -c "import PACKAGE_NAME; print(PACKAGE_NAME.__file__)"` | Check the package's location. |
| `/opt/ml/bin/python -m pip list` | List shared packages. |
| `deactivate` | Deactivate the environment. |

---
#### Happy computing and good luck with your research!
---