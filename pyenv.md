# **Pyenv Handbook**

**Pyenv** is a Python version management tool that allows you to seamlessly switch between multiple Python versions on the same machine. It simplifies installing, managing, and using multiple Python interpreters without interfering with the system Python.

---

## **1. What is Pyenv?**

### Key Features:
1. **Manage Multiple Python Versions**: Easily switch between Python versions.
2. **Install Any Python Version**: Supports CPython, Anaconda, Miniconda, PyPy, and more.
3. **Avoid System Python Interference**: Keeps system Python untouched.
4. **Local Project-Specific Python Versions**: Use different Python versions for different projects.

---

## **2. Installation**

### Prerequisites
- Ensure you have:
  - **`git`**  
  - **`curl`**, **`build-essential`** (Linux)  
  - **Homebrew** (macOS, optional)

### Install Pyenv (Linux/macOS)
Use the installation script:
```bash
curl https://pyenv.run | bash
```

### Add Pyenv to Your Shell (bash/zsh):
Add these lines to your `~/.bashrc`, `~/.bash_profile`, or `~/.zshrc`:
```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```

Apply changes:
```bash
source ~/.bashrc   # or ~/.zshrc
```

### Verify Installation
```bash
pyenv --version
```

---

## **3. Installing Python Versions**

### List Available Versions
```bash
pyenv install --list
```

### Install a Specific Python Version
```bash
pyenv install 3.11.5
```

### Install the Latest Version
```bash
pyenv install 3.12.0
```

---

## **4. Managing Python Versions**

### Show Installed Versions
```bash
pyenv versions
```

### Set the Global Python Version
Set a default version for all projects:
```bash
pyenv global 3.11.5
```

### Set a Local Python Version
Use a specific version in a directory:
```bash
pyenv local 3.9.7
```
This creates a `.python-version` file in the directory.

### Use a Specific Version Temporarily
```bash
pyenv shell 3.10.4
```

---

## **5. Checking Python Version**

### Check Current Version
```bash
python --version
```

### Verify Pyenv's Python is Active
```bash
which python
```

It should point to Pyenv's Python:
```
~/.pyenv/shims/python
```

---

## **6. Managing Python Versions in Projects**

### Create a Project-Specific Python Version
Navigate to your project folder:
```bash
cd my_project
pyenv local 3.9.7
```

### Verify Local Version
```bash
python --version
```

---

## **7. Managing Virtual Environments**

You can integrate Pyenv with `pyenv-virtualenv` to manage virtual environments.

### Install pyenv-virtualenv
```bash
git clone https://github.com/pyenv/pyenv-virtualenv.git \
  $(pyenv root)/plugins/pyenv-virtualenv
```

Add this to your shell configuration:
```bash
eval "$(pyenv virtualenv-init -)"
```
Reload your shell:
```bash
source ~/.bashrc   # or ~/.zshrc
```

---

### **Creating Virtual Environments**

#### Create a Virtual Environment
```bash
pyenv virtualenv 3.11.5 my-env
```

#### List Virtual Environments
```bash
pyenv virtualenvs
```

#### Activate a Virtual Environment
```bash
pyenv activate my-env
```

#### Deactivate the Virtual Environment
```bash
pyenv deactivate
```

#### Remove a Virtual Environment
```bash
pyenv uninstall my-env
```

---

### Use a Virtual Environment in a Project
To associate a virtual environment with a project:
```bash
pyenv local my-env
```
This adds the virtual environment name to the `.python-version` file.

---

## **8. Useful Pyenv Commands**

| **Command**                         | **Description**                                 |
|-------------------------------------|-------------------------------------------------|
| `pyenv install --list`              | List all available Python versions              |
| `pyenv install <version>`           | Install a specific Python version               |
| `pyenv versions`                    | Show all installed Python versions              |
| `pyenv uninstall <version>`         | Uninstall a specific Python version             |
| `pyenv global <version>`            | Set the global Python version                   |
| `pyenv local <version>`             | Set a local Python version in a directory       |
| `pyenv shell <version>`             | Use a specific version temporarily              |
| `pyenv virtualenv <ver> <name>`     | Create a virtual environment                    |
| `pyenv virtualenvs`                 | List all virtual environments                   |
| `pyenv activate <name>`             | Activate a virtual environment                  |
| `pyenv deactivate`                  | Deactivate the current environment              |
| `pyenv which python`                | Check which Python executable is being used     |
| `pyenv rehash`                      | Rehash to recognize newly installed versions    |

---

## **9. Troubleshooting**

### Common Issues

#### **`pyenv: command not found`**
Ensure Pyenv is added to your shell profile:
```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
```

#### **Python Build Fails**
Install dependencies (Linux):
```bash
sudo apt-get update
sudo apt-get install -y build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev \
python-openssl git
```

#### **Pyenv Not Switching Versions**
Run:
```bash
pyenv rehash
```

Ensure there is no system-wide Python interfering.

---

## **10. Workflow Example**

### Step 1: Install Python Versions
```bash
pyenv install 3.9.7
pyenv install 3.11.5
```

### Step 2: Set a Global Python Version
```bash
pyenv global 3.11.5
```

### Step 3: Create a Project-Specific Python Version
```bash
mkdir my_project && cd my_project
pyenv local 3.9.7
```

### Step 4: Create and Activate a Virtual Environment
```bash
pyenv virtualenv 3.9.7 my-env
pyenv activate my-env
```

### Step 5: Verify Python Version
```bash
python --version
```

---

## **11. Integrations**

### Use Pyenv with IDEs

#### **VS Code**
1. Install the **Python Extension**.
2. Set the Python interpreter to Pyenv's version:
   ```bash
   pyenv which python
   ```
3. Use the path in VS Code's interpreter settings.

#### **PyCharm**
- Go to **Settings > Project Interpreter**.
- Add a new interpreter using the path:
  ```bash
  ~/.pyenv/versions/<version>/bin/python
  ```

---

## **12. Additional Tools**

- **pyenv-virtualenvwrapper**: Combine `virtualenvwrapper` and `pyenv`.
- **pyenv-doctor**: Diagnose installation problems.
  ```bash
  pyenv doctor
  ```

---

## **13. Summary of Workflow**

1. **Install Pyenv** and required dependencies.  
2. **Install Python versions** using `pyenv install`.  
3. **Set global or local versions** with `pyenv global` or `pyenv local`.  
4. **Create virtual environments** with `pyenv virtualenv`.  
5. **Activate and deactivate environments** with `pyenv activate` and `pyenv deactivate`.  
6. **Verify Python version** and project setup.

---

## **14. Resources**

- **Official Documentation**: [https://github.com/pyenv/pyenv](https://github.com/pyenv/pyenv)  
- **pyenv-virtualenv**: [https://github.com/pyenv/pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)  
- **Python Installation Dependencies**: [Pyenv Wiki](https://github.com/pyenv/pyenv/wiki)  

---

With Pyenv, you can efficiently manage multiple Python versions, isolate project environments, and simplify your development workflow.
