# Python Project Setup Notes

## 1. Creating a Virtual Environment
```bash
# Create a virtual environment named '.venv'
python -m venv .venv

# Activate the virtual environment (Windows)
.venv\Scripts\activate

# Activate the virtual environment (Linux/Mac)
source .venv/bin/activate

# Deactivate the virtual environment
.venv\Scripts\deactivate  # Windows
deactivate                # Linux/Mac
```

## 2. Managing Packages
```bash
# Upgrade pip to the latest version
pip install --upgrade pip

# Install packages from requirements.txt
pip install -r requirements.txt

# Freeze current environment packages into requirements.txt
pip freeze > requirements.txt

# Install a specific package
pip install package_name

# Uninstall a package
pip uninstall package_name
```

## 3. Checking Python and Pip Information
```bash
# Check Python executable location
where python     # Windows
which python     # Linux/Mac

# Check Python version
python --version

# Check pip version
pip --version
```

## 4. Additional Virtual Environment Commands
```bash
# Create virtual environment with specific Python version
python3.9 -m venv .venv

# List installed packages
pip list

# Show details of an installed package
pip show package_name

# Check for outdated packages
pip list --outdated

# Upgrade a specific package
pip install --upgrade package_name
```

## 5. Best Practices
- Use a virtual environment for each project to manage dependencies.
- Always freeze dependencies with `pip freeze > requirements.txt` before sharing the project.
- Regularly update packages to keep them secure and compatible.
- Use `python -m venv` instead of `virtualenv` for simplicity (built-in since Python 3.3).

