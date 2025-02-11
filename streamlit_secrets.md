# Configuring Streamlit secrets

If you don't create this secrets file, no problem. Its optional. only your secret key is exposed for public/teams to see if repo is not private.

## Overview
When programming I included my `.streamlit\secrets.toml` in `.gitignore` file.
So, it is not available in the repo. you need to create one. This file is for keeping
secrets away when it comes to deployment on streamlit cloud and working with teams and locally.

you can also keep this .streamlit folder in your users folder as
`C:\Users\%username%\.streamlit\secrets.toml` this one is considered as global.

**If you have both files on project root and in the user_folder it will accept the project root one.**

The another on the local projects folder was considered as per-project secrets.
When both file co-exists the local one will overwrite the global.
Example of Streamlit.toml

```bash
# .streamlit\secrets.toml

#you can have multiple configuration in toml                            
MySQL_URL = 'mysql+pymysql://user:password@host:port/database' 
API_key = '<API Key>'
MONGO_DDB_URI = '<MongoDB URI>'

[default-settings]
defalt_list = ['Some','list', 'for','access']
color = blue
# other settings can be palaced here.
```

## syntax
- mention the variable_name and key as simple as python syntax.
    ```bash
    API_key = '<API Key>'
    ```
- if secrets need to be separate, you can separate them using the following syntax.
    ```bash
    [default-settings]
    d_channel = st.secrets["default_settings"]["default_channel"]
    ```
- finally, secrets needs comments for identification or other needs. you can just start with `# ` for commenting.
    ```bash
    # --- comments here ---
    ```
## how to access 
- Accessing streamlit was not a problem you can use the following syntax.
    ```bash
    secret_key = st.secrets[Key_name]
    ```
- what if the secret was separated with `[title]`.
    ```bash
    color_system = st.secrets["default_settings"]["color"]
    ```
If the key is missing on the file it might throw KeyError, you can write exception for that.