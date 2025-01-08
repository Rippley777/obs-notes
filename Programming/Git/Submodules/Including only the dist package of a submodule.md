Including only the `dist` package of a repository as a **submodule** can make sense in specific scenarios, particularly if you want to use the built output of a library or tool without needing to manage its source code. However, submodules typically link to the entire repository, so additional steps are required if you want to include only the `dist` directory.

Here are some considerations and approaches to achieve this:

---

### Scenarios Where Including Only `dist` Makes Sense

1. **Pre-built Libraries or Tools**:
    
    - You only need the compiled/built assets (e.g., JavaScript bundles, CSS files) for use in your project.
    - You do not need the source code or development dependencies.
2. **Minimizing Repository Clutter**:
    
    - Keeping the main repository clean by including only the `dist` folder from a submodule.
3. **Deployments or Static Asset Inclusion**:
    
    - Using the pre-built `dist` directory as static assets for deployment.

---

### Ways to Achieve This

#### Option 1: Use a Separate Branch for `dist` (Preferred)

You can configure the submodule repository to maintain a separate branch containing only the `dist` directory.

1. **Set Up the Submodule Repository**:
    
    - In the submodule repository, create a new branch (e.g., `dist-only`) containing only the `dist` folder.
    - Example commands for the submodule repository:
        
        bash
        
        Copy code
        
        `git checkout --orphan dist-only git reset --hard git add dist git commit -m "Add dist-only branch with pre-built files" git push origin dist-only`
        
2. **Add the Submodule to Your Main Repository**:
    
    - Add the submodule and specify the `dist-only` branch:
        
        bash
        
        Copy code
        
        `git submodule add -b dist-only <repository_url> <submodule_path>`
        
    - Example:
        
        bash
        
        Copy code
        
        `git submodule add -b dist-only https://github.com/username/library.git libs/library`
        
3. **Commit Changes**:
    
    bash
    
    Copy code
    
    `git add .gitmodules libs/library git commit -m "Added library submodule with dist-only branch"`
    

---

#### Option 2: Include Full Repository but Only Use `dist`

If the submodule does not have a `dist-only` branch:

1. Add the submodule as usual:
    
    bash
    
    Copy code
    
    `git submodule add <repository_url> <submodule_path>`
    
2. Ignore unnecessary files or directories in your workflow:
    
    - Use `.gitignore` or build scripts to exclude non-dist files when bundling or deploying.

---

#### Option 3: Copy `dist` Files Instead of Using a Submodule

If you don’t need the full benefits of submodules, you can automate copying the `dist` folder from the other repository:

1. Use a tool like `curl`, `wget`, or `git archive` to fetch just the `dist` files:
    
    bash
    
    Copy code
    
    `curl -L <repository_url>/archive/refs/heads/main.zip -o repo.zip unzip repo.zip cp -r repo-main/dist ./libs/library`
    
2. Automate this process in your CI/CD pipeline or a build script.
    

---

### Drawbacks of Including Only `dist`

- **Loss of Source Context**:
    
    - You won’t have access to the source code or history, which can make debugging harder.
- **Updates Require Rebuilding**:
    
    - Someone must ensure the `dist` branch or directory is up-to-date.
- **More Maintenance**:
    
    - Keeping a `dist-only` branch synced with the main repository can require extra effort.

---

### Summary

If you want to include only the `dist` directory:

- **Preferred**: Use a `dist-only` branch in the submodule repository.
- **Alternative**: Use scripts or CI/CD to fetch or copy just the `dist` directory.