### 1. **Install the Desired Node Version**

First, ensure you have the desired Node.js version installed:

bash

Copy code

`nvm install <version>`

For example:

bash

Copy code

`nvm install 18`

---

### 2. **Set the Default Node Version**

#### Option 1: Use `nvm alias default`

Set the default version globally:

bash

Copy code

`nvm alias default <version>`

For example:

bash

Copy code

`nvm alias default 18`

This will make Node.js version `18` the default for all new shells.

---

### 3. **Verify the Default Version**

After setting the default, you can verify it:

bash

Copy code

`nvm ls`

The output will show something like this:

rust

Copy code

       `v16.20.0 ->     v18.17.0 default -> 18 (-> v18.17.0) node -> stable (-> v18.17.0) (default) stable -> 18.17 (-> v18.17.0) (default)`

The arrow (`->`) and `default` indicate the currently active and default versions.

---

### 4. **Activate the Default Version**

To ensure the default version is used in the current shell session:

bash

Copy code

`nvm use default`

---

### 5. **Automatically Use the Default Version in New Shells**

Make sure your shell’s startup file (`.bashrc`, `.zshrc`, etc.) is correctly configured to load `nvm`. Add the following line if it’s missing:

bash

Copy code

`export NVM_DIR="$HOME/.nvm" [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"`

This will automatically load the default version when opening a new terminal session.

---

### 6. **Optional: Per-Project Node Version**

If you want to set a specific Node.js version for a project:

1. Inside the project directory, create an `.nvmrc` file:
    
    bash
    
    Copy code
    
    `echo "18" > .nvmrc`
    
2. Use the `.nvmrc` version in the project:
    
    bash
    
    Copy code
    
    `nvm use`