# uv, pip & conda

Think of Python development as building an application that depends on multiple tools and libraries. 
You need a way to install those libraries, manage Python versions, and prevent one project's dependencies from breaking another project.

## pip

`pip` installs Python packages, usually from the Python Package Index (PyPI). 
It is the traditional package installer included with most Python installations.

```bash
# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
# Windows
.venv\Scripts\activate

# Linux/Mac
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

## uv

`uv` is a blazing-fast Python package and project manager written in Rust. 

It can install packages, create virtual environments, manage Python versions, and manage project dependencies and lockfiles.

```bash
# Create a virtual environment
uv venv

# Activate the virtual environment
# Windows
.venv\Scripts\activate

# Linux/Mac
source .venv/bin/activate

# Install dependencies
uv pip install -r requirements.txt

# Install a single package
uv pip install requests

# Verify the installation
uv pip list

# Check Python version
python --version
```

## Conda

`conda` is a package manager and environment management system for Python, R, and other languages. 
It is widely used in data science and scientific computing.

```bash
# Create a conda environment
conda create --name myenv python=3.9

# Activate the conda environment
conda activate myenv

# Install dependencies
conda install -r requirements.txt
```


# Imagine your Python project is a kitchen.

- Python = the kitchen itself.
- Packages = ingredients you need.
- Package manager = the person who gets the ingredients.
- Virtual environment = a separate kitchen for each project.

**The key distinction is that pip primarily installs Python packages, uv provides a faster, broader Python development workflow, and conda can manage Python plus non-Python dependencies**