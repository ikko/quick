# **Python Poetry Handbook**

Poetry is a modern dependency management and packaging tool for Python. It simplifies project dependency management, virtual environments, and package distribution.

---

## **1. Installation**

### Prerequisites
Ensure Python (>= 3.7) and pip are installed.

### Install Poetry
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

### Verify Installation
```bash
poetry --version
```

### Add Poetry to Path
For manual setup, add Poetry to your shell profile:
```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

## **2. Key Features**

- **Dependency Management**: Handles project dependencies efficiently.  
- **Virtual Environment Management**: Automatically creates isolated environments.  
- **Build and Publish**: Easily package and publish projects to PyPI.  
- **Version Management**: Simplifies dependency version resolution.  

---

## **3. Creating and Managing Projects**

### **Create a New Project**
```bash
poetry new project-name
```
This creates a structure like:
```
project-name/
├── pyproject.toml
├── README.rst
├── project_name/
│   └── __init__.py
└── tests/
```

### **Add Poetry to an Existing Project**
If your project already exists:
```bash
poetry init
```
This will interactively generate a `pyproject.toml` file.

---

## **4. pyproject.toml File**

### **Purpose**
The `pyproject.toml` is the central configuration file for Poetry. It defines project metadata, dependencies, and settings.

### Example pyproject.toml
```toml
[tool.poetry]
name = "my_project"
version = "0.1.0"
description = "A sample Python project using Poetry"
authors = ["Your Name <your@email.com>"]
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.9"
requests = "^2.25.1"

[tool.poetry.dev-dependencies]
pytest = "^6.2.2"
black = "^23.3.0"

[build-system]
requires = ["poetry-core>=1.0.0"]
build-backend = "poetry.core.masonry.api"
```

---

## **5. Dependency Management**

### **Add a Dependency**
```bash
poetry add <package-name>
```
Example:
```bash
poetry add requests
```

### **Add Development Dependencies**
```bash
poetry add --dev pytest
```

### **Remove a Dependency**
```bash
poetry remove <package-name>
```

### **Update Dependencies**
Update all dependencies:
```bash
poetry update
```
Update a specific package:
```bash
poetry update <package-name>
```

### **View Current Dependencies**
```bash
poetry show
```

---

## **6. Virtual Environments**

### **Check the Virtual Environment**
Poetry creates a virtual environment automatically.  
Check the current environment:
```bash
poetry env info
```

### **Activate the Environment**
```bash
poetry shell
```

### **Run Commands in the Virtual Environment**
Without activating the shell:
```bash
poetry run <command>
```
Example:
```bash
poetry run python script.py
```

### **Remove the Virtual Environment**
```bash
poetry env remove <python-version>
```

---

## **7. Build and Publish Packages**

### **Build Your Package**
```bash
poetry build
```
Output:
```
dist/
├── my_project-0.1.0.tar.gz
└── my_project-0.1.0-py3-none-any.whl
```

### **Publish to PyPI**
```bash
poetry publish --build
```

### **Publish to a Private Registry**
Specify a custom repository:
```bash
poetry config repositories.<name> <url>
poetry publish -r <name>
```

---

## **8. Version Management**

### **Bump the Version**
Update the project version automatically:
```bash
poetry version <rule>
```
- `patch`: Increment patch version (e.g., 0.1.0 -> 0.1.1)  
- `minor`: Increment minor version (e.g., 0.1.0 -> 0.2.0)  
- `major`: Increment major version (e.g., 0.1.0 -> 1.0.0)  

Example:
```bash
poetry version patch
```

---

## **9. Working with Lock Files**

- Poetry generates a `poetry.lock` file to lock dependencies and their versions.
- Always commit `poetry.lock` to version control for consistency.

### **Install Locked Dependencies**
Install dependencies exactly as specified in the lock file:
```bash
poetry install
```

### **Regenerate the Lock File**
```bash
poetry lock --no-update
```

---

## **10. Scripts and Custom Commands**

### Add Custom Scripts
Define scripts in the `pyproject.toml`:
```toml
[tool.poetry.scripts]
start = "my_project.main:main"
```

Run the script:
```bash
poetry run start
```

---

## **11. Useful Poetry Commands**

| **Command**                          | **Description**                            |
|--------------------------------------|--------------------------------------------|
| `poetry new <project>`               | Create a new project                       |
| `poetry init`                        | Add Poetry to an existing project          |
| `poetry add <package>`               | Add a dependency                           |
| `poetry remove <package>`            | Remove a dependency                        |
| `poetry install`                     | Install project dependencies               |
| `poetry update`                      | Update project dependencies                |
| `poetry build`                       | Build the project package                  |
| `poetry publish`                     | Publish the package to PyPI                |
| `poetry shell`                       | Activate the virtual environment           |
| `poetry run <command>`               | Run a command in the Poetry environment    |
| `poetry show`                        | Show installed dependencies                |
| `poetry lock`                        | Update or regenerate the lock file         |
| `poetry version <rule>`              | Update project version                     |
| `poetry env info`                    | Show virtual environment information       |

---

## **12. Integrating Poetry with Other Tools**

### **PyCharm**
1. Go to **Settings > Project Interpreter**.  
2. Set the Python interpreter to the Poetry virtual environment.  

Locate the environment with:
```bash
poetry env info --path
```

### **VSCode**
1. Install the **Python extension**.  
2. Select the Poetry virtual environment under the Python interpreter settings.

---

## **13. Migrating from pip or pipenv**

### Migrate from `requirements.txt`
```bash
poetry add $(cat requirements.txt)
```

### Migrate from Pipenv
Convert `Pipfile` to `pyproject.toml`:
```bash
poetry import
```

---

## **14. Troubleshooting**

### Missing Virtual Environment
Regenerate the environment:
```bash
poetry install
```

### Dependency Conflicts
Resolve conflicts by inspecting `pyproject.toml` and running:
```bash
poetry update
```

### Installing a Specific Python Version
```bash
poetry env use python3.9
```

---

## **15. Resources**

- **Official Documentation**: [https://python-poetry.org/docs/](https://python-poetry.org/docs/)  
- **GitHub Repository**: [https://github.com/python-poetry/poetry](https://github.com/python-poetry/poetry)  
- **CLI Reference**: [https://python-poetry.org/docs/cli/](https://python-poetry.org/docs/cli/)

---

This handbook provides an overview of Poetry's features and usage for dependency management, virtual environments, and packaging. Poetry streamlines project workflows and is a must-have tool for modern Python development.
