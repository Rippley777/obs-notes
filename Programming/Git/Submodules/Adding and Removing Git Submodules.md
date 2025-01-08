### 1. **Navigate to Your Repository**

Navigate to the root directory of your project where you want to add the submodule.

bash

Copy code

`cd /path/to/your/project`

---

### 2. **Add the Submodule**

Use the following command to add the UI components repository as a submodule:

bash

Copy code

`git submodule add <repository-url> <path>`

- `<repository-url>`: URL of the repository you want to add (e.g., `https://github.com/user/ui-components.git`).
- `<path>`: (Optional) The directory where the submodule will reside. By default, it will use the repository name.

Example:

bash

Copy code

`git submodule add https://github.com/user/ui-components.git src/ui-components`

---

### 3. **Initialize and Update Submodules**

After adding the submodule, initialize and fetch the contents:

bash

Copy code

`git submodule init git submodule update`

---

### 4. **Commit the Changes**

Commit the new submodule to your repository:

bash

Copy code

`git add .gitmodules src/ui-components git commit -m "Add UI components as a submodule"`

---

### 5. **Working with Submodules**

#### **Cloning the Repository with Submodules**

When someone clones your repository, they must also initialize and update the submodules:

bash

Copy code

`git clone <repository-url> cd <project-directory> git submodule update --init --recursive`

#### **Pulling Updates from Submodules**

If the submodule's source repository is updated, pull the latest changes:

bash

Copy code

`cd src/ui-components git pull origin main`

Then commit the submodule update in the main repository:

bash

Copy code

`cd ../.. git add src/ui-components git commit -m "Update UI components submodule"`

#### **Switching Submodule Branch**

By default, submodules are linked to a specific commit. To track a specific branch instead:

bash

Copy code

`cd src/ui-components git checkout main`

Then update `.gitmodules` to track a branch:

bash

Copy code

`[submodule "src/ui-components"]     path = src/ui-components     url = https://github.com/user/ui-components.git     branch = main`

Commit the `.gitmodules` changes:

bash

Copy code

`git add .gitmodules git commit -m "Track main branch for UI components"`

---

### 6. **Removing a Submodule**

To remove a submodule if it’s no longer needed:

1. Remove the submodule entry from `.gitmodules`:
    
    bash
    
    Copy code
    
    `git config -f .gitmodules --remove-section submodule.src/ui-components`
    
2. Remove the submodule from the `.git/config`:
    
    bash
    
    Copy code
    
    `git config --remove-section submodule.src/ui-components`
    
3. Delete the submodule directory and its references:
    
    bash
    
    Copy code
    
    `rm -rf src/ui-components git rm --cached src/ui-components git commit -m "Remove UI components submodule"`
    

---

### 7. **Alternative: Use a Package Manager**

If you prefer not to use submodules, consider using a package manager like `npm` or `yarn` to version and distribute your UI components as a library.