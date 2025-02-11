# Configuring Streamlit secrets

Keeping your secret keys needs to be first priority. If secret key is exposed. 
It might get the project in danger by giving unwanted anonymous users access. 
People with paid API might lose their money. If it was corporate it will be even worse. 
There are multiple ways for saving it in project. the most common for small project follows, 

## using `python-dotenv`
- When using this method. It loads all the data in the file as `environment variables` for the project locally. 
- The most common way is to use `.env` file. `.` makes this file hidden.

- ***The most important when using this method is adding this `.env` file to `.gitignore` file.***
If not added, doing this step is vain.
``` python
# .env file

# Database configuration
DATABASE_URL=postgres://user:password@localhost:5432/mydatabase

# API keys
API_KEY='<your_api_key_here>' # quotes makes it as string
SECRET_KEY="your_secret_key_here"

# Debug mode
DEBUG=True

# Port number
PORT=8000

# Multi-line value
MULTILINE="Line one.\nLine two."

# Empty value
EMPTY_KEY=

# Special characters
SPECIAL="This # is a special value = with spaces"
```

### syntax for `.env`
* create a file named `.env`. no file extension.
* mention the variable_name and key as simple as python syntax.
    ``` python
    API_KEY='<your_api_key_here>'
    ```
  It can have the following values.
  - numbers
  - strings
  - multiline strings
  - empty value
  - boolean
* if secrets need to be separate, you can separate them using the following syntax.
    ``` python
    [default-settings]
    d_channel = st.secrets["default_settings"]["default_channel"]
    ```
* finally, secrets needs comments for identification or other needs. you can just start with `# ` for commenting.
    ``` python
    # --- comments here ---
    ```
  
### how to access
- First the data need to be loaded in, It was done by `python-dotenv` module.
  - Install the module using pip
    ``` bash
    python3 -m pip install python-dotenv
    ```
  - load the data as local environments.
    ``` python
    from dotenv import load_dotenv
    
    # Load the .env file
    load_dotenv()
    
    # now all the variavles in that .env file 
    # was available as environment variables
    ```
- Accessing environment variables.
  ``` python 
  import os
  
  # Access the environment variables
  database_url = os.getenv('DATABASE_URL')
  
  # Use the variables
  print(f"Database URL: {database_url}")
  ```
If the key is missing on the file it will not throw any error, instead it will return `None`.

**Example**
``` python
from dotenv import load_dotenv
import os

# Load the .env file
load_dotenv()

# Access the environment variables
database_url = os.getenv('DATABASE_URL')
api_key = os.getenv('API_KEY')
secret_key = os.getenv('SECRET_KEY')
debug_mode = os.getenv('DEBUG', default=False)  # Default value if not found

# Use the variables
print(f"Database URL: {database_url}")
print(f"API Key: {api_key}")
print(f"Secret Key: {secret_key}")
print(f"Debug Mode: {debug_mode}")
```


## secret file method

- In this method, create a file name then **add it to `.gitignore`** for not pushing it to repo.
- Adding `.` before the file will make hidden from the file manager.
- you can have file extension like `*.txt`, `*.json` or leave it without extension.

  - ### with json file

    - create json file i'm creating as `secrets.json`.
      ``` json
      {
        "DATABASE_URL": "postgres://user:password@localhost:5432/mydatabase",
        "API_KEY": "your_api_key_here",
        "SECRET_KEY": "your_secret_key_here",
        "DEBUG": true,
        "PORT": 8000
      }
      ```
      
    - Load and read the JSON File in Python
      ``` python
      import json

      # Path to the JSON file
      secrets_file = 'secrets.json'
    
      # Load the JSON file
      with open(secrets_file, 'r') as file:
          secrets = json.load(file)
    
      # Access the secrets
      database_url = secrets['DATABASE_URL']
      api_key = secrets['API_KEY']
      secret_key = secrets['SECRET_KEY']
      debug_mode = secrets['DEBUG']
      port = secrets['PORT']
    
      # Use the secrets
      print(f"Database URL: {database_url}")
      print(f"API Key: {api_key}")
      print(f"Secret Key: {secret_key}")
      print(f"Debug Mode: {debug_mode}")
      print(f"Port: {port}")
      ```
    - In this attempt you can encounter following errors
      - `FileNotFoundError`
      - `json.JSONDecodeError`
      - `Exception`
  
  - ### with text file
  
    - create `.secrets.txt` file
      ``` text
      # secrets.txt
      DATABASE_URL=postgres://user:password@localhost:5432/mydatabase
      API_KEY=your_api_key_here
      SECRET_KEY=your_secret_key_here
      DEBUG=True
      PORT=8000
      ```
    - Load and read Text file in python. 
      ``` python
      # Path to the text file
      secrets_file = 'secrets.txt'

      # Initialize an empty dictionary to store secrets
      secrets = {}

      # Read the text file
      with open(secrets_file, 'r') as file:
      for line in file:
          # Skip comments and empty lines
          if line.strip() and not line.startswith('#'):
              # Split the line into key and value
              key, value = line.strip().split('=', 1)  # Split on the first '='
              secrets[key.strip()] = value.strip()

      # Access the secrets
      database_url = secrets.get('DATABASE_URL')
      api_key = secrets.get('API_KEY')
      secret_key = secrets.get('SECRET_KEY')
      debug_mode = secrets.get('DEBUG')
      port = secrets.get('PORT')

      # Use the secrets
      print(f"Database URL: {database_url}")
      print(f"API Key: {api_key}")
      print(f"Secret Key: {secret_key}")
      print(f"Debug Mode: {debug_mode}")
      print(f"Port: {port}")
      ```
    - you can face following errors, you can wire exceptions here.
      - `FileNotFoundError`
      - `json.JSONDecodeError`
      - `Exception` 