# Jupyter Kernel Management in Virtual Environment
---

### 1. Create a Virtual Environment

creates a virtual environment named 'myenv':
  ```bash
  python -m venv myenv
  ```

### 2. Activate the Virtual Environment
- **On Windows:**
  ```bash
  myenv\Scripts\activate
  ```
- **On Linux/macOS:**
  ```bash
  source myenv/bin/activate
  ```

### 3. Install Jupyter in the Virtual Environment
  - Installs Jupyter to manage notebooks within this environment
  ```bash
  pip install jupyter
  ```

### 4. Add the Virtual Environment as a New Jupyter Kernel
  ```bash
  python -m ipykernel install --user --name=myenv --display-name "Python (myenv)"
  ```
- `--user`: installs the kernel for the current user
- `--name`: internal name for the kernel
- `--display-name`: name displayed in Jupyter

### 5. Verify Installed Jupyter Kernels
  Lists all installed kernels with their paths
  ```bash
  jupyter kernelspec list
  ```

### 6. Launch Jupyter Notebook
  ```bash   
  jupyter notebook
  ```
  Opens Jupyter Notebook in your default browser

### 7. Delete/Remove a Jupyter Kernel
  ```bash
  jupyter kernelspec uninstall myenv
  ```
  This removes the 'myenv' kernel from Jupyter without affecting the virtual environment itself

### 8. Deactivate the Virtual Environment
  ```bash
  deactivate
  ```
  Exits the virtual environment, returning to the system Python

