### **For Arch Linux (using `pacman`):**

1. Open the container shell:
    `docker exec -it <container_name> /bin/bash`
    
    Or if starting a new container:
    
    `docker run -it archlinux /bin/bash`
    
2. Update the package database:
    `pacman -Syu`
    
3. Install `vi` (usually provided by the `vim` package):
    
    `pacman --noconfirm --needed -S vim`
    
4. Verify the installation:
    
    `vi --version`
    

---

### **For Other Distributions:**

#### **Debian/Ubuntu (using `apt`):**

`apt-get update apt-get install -y vim`

#### **Fedora (using `dnf`):**
`dnf install -y vim`

#### **Alpine Linux (using `apk`):**
`apk add vim`

---

### **Testing the Installation**

After installing, you can use `vi` by typing:
`vi`