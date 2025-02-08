# Jupyter Kernel Management in Virtual Environment

```bash
# 1. Create a Virtual Environment
python -m venv myenv  # Creates a virtual environment named 'myenv'

# 2. Activate the Virtual Environment
# On Windows:
myenv\Scripts\activate
# On Linux/macOS:
source myenv/bin/activate

# 3. Install Jupyter in the Virtual Environment
pip install jupyter  # Installs Jupyter to manage notebooks within this environment

# 4. Add the Virtual Environment as a New Jupyter Kernel
python -m ipykernel install --user --name=myenv --display-name "Python (myenv)"
# --user: installs the kernel for the current user
# --name: internal name for the kernel
# --display-name: name displayed in Jupyter

# 5. Verify Installed Jupyter Kernels
jupyter kernelspec list  # Lists all installed kernels with their paths

# 6. Launch Jupyter Notebook
jupyter notebook  # Opens Jupyter Notebook in your default browser

# 7. Delete/Remove a Jupyter Kernel
jupyter kernelspec uninstall myenv
# This removes the 'myenv' kernel from Jupyter without affecting the virtual environment itself

# 8. Deactivate the Virtual Environment
deactivate  # Exits the virtual environment, returning to the system Python
```

