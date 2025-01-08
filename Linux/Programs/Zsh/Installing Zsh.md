### **Step 1: Check if Zsh is already installed**

1. Open a terminal.
2. Run the command:
    
    `zsh --version`
    
    If Zsh is installed, you'll see the version. If not, proceed to install it.

---

### **Step 2: Install Zsh**

#### **For Debian-based distributions (Ubuntu, Debian, etc.)**

1. Update package lists:

    `sudo apt update`
    
2. Install Zsh:
    
    `sudo apt install zsh -y`
    

#### **For Red Hat-based distributions (Fedora, CentOS, RHEL, etc.)**

1. Install Zsh:
    
    `sudo dnf install zsh -y`
    

#### **For Arch-based distributions (Arch Linux, Manjaro, etc.)**

1. Install Zsh:
    
    `sudo pacman -S zsh`
    

#### **For openSUSE**

1. Install Zsh:
    
    `sudo zypper install zsh`
    

#### **For Gentoo**

1. Install Zsh:
    
    `sudo emerge zsh`
    

---

### **Step 3: Set Zsh as the default shell**

1. Change your default shell to Zsh:
    
    `chsh -s $(which zsh)`
    
2. Log out and log back in for the change to take effect.

---

### **Step 4: Customize Zsh (optional)**

For a better experience, you can install a framework like **Oh My Zsh**:

1. Install **Oh My Zsh**:
    
    `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
    
2. Follow the prompts to complete the installation.