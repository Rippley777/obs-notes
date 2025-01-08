### **Step 1: Start or Access the Container**

If you already have a container running:
`docker exec -it <container_name> /bin/bash`

If you need to start a new Arch Linux container:

`docker run -it archlinux /bin/bash`

---

### **Step 2: Update the Package Database**

Ensure the package database is up-to-date:
`pacman -Syu`

---

### **Step 3: Install Git**

Install Git using `pacman`:

`pacman --noconfirm --needed -S git`

---

### **Step 4: Verify the Installation**

Check the installed Git version to confirm:

`git --version`

You should see the version output, confirming Git is installed.

---

### **Notes:**

- If you're using a non-Arch-based container, the installation command will depend on the distribution:
    - **Debian/Ubuntu**: `apt-get install -y git`
    - **Fedora**: `dnf install -y git`
    - **Alpine**: `apk add git`