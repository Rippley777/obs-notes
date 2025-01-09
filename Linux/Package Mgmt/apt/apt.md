```shell-session
apt-cache search impacket

impacket-scripts - Links to useful impacket scripts examples
polenum - Extracts the password policy from a Windows system
python-pcapy - Python interface to the libpcap packet capture library (Python 2)
python3-impacket - Python3 module to easily build and dissect network protocols
python3-pcapy - Python interface to the libpcap packet capture library (Python 3)
```
----------------------------------------

`dpkg` is a low-level package manager for Debian-based systems, used to install, remove, and manage `.deb` packages. It's an essential tool for managing software, particularly when higher-level tools like `apt` are unavailable or unsuitable.

---

## Key Features of `dpkg`

1. **Low-Level Control**: Provides direct access to package management.
    
2. **Debian-Specific**: Handles `.deb` packages directly.
    
3. **Script Execution**: Runs pre-installation and post-installation scripts included in packages.
    
4. **Offline Usage**: Can be used without a network connection since it doesn’t resolve dependencies automatically.
    

---

## Basic Usage

### Installing a Package

To install a `.deb` package:

```
sudo dpkg -i package_name.deb
```

- `-i`: Stands for `--install`.
    

---

### Removing a Package

To remove a package:

```
sudo dpkg -r package_name
```

- `-r`: Stands for `--remove`. Keeps configuration files intact.
    

To remove configuration files as well:

```
sudo dpkg -P package_name
```

- `-P`: Stands for `--purge`.
    

---

### Listing Installed Packages

To see all installed packages:

```
dpkg -l
```

- **Common Output Columns**:
    
    - `ii`: Installed successfully.
        
    - `rc`: Removed, but configuration files remain.
        
    - `un`: Not installed but referenced in the system.
        

---

### Querying a Package

To check if a package is installed:

```
dpkg -s package_name
```

- `-s`: Stands for `--status`.
    

To find out which files a package installed:

```
dpkg -L package_name
```
impa
- `-L`: Stands for `--listfiles`.
    

---

### Verifying Installed Files

To verify if package files are still intact:

```
dpkg --verify package_name
```

- Compares the files installed by the package to the system’s current state.
    

---

### Extracting Package Contents

To extract the contents of a `.deb` package without installing it:

```
dpkg -x package_name.deb /path/to/extract
```

- `-x`: Stands for `--extract`.
    

To extract and control package metadata as well:

```
dpkg -e package_name.deb /path/to/extract
```

- `-e`: Stands for `--control`.
    

---

### Reconfiguring a Package

If a package's setup needs to be redone:

```
sudo dpkg-reconfigure package_name
```

- Reruns configuration scripts for the package.
    

---

## Common Issues and Fixes

### Missing Dependencies

`dpkg` does not resolve dependencies automatically. If a dependency is missing, the installation might fail with an error like:

```
dependency problems - leaving unconfigured
```

To fix this, use `apt` to resolve dependencies:

```
sudo apt-get install -f
```

- `-f`: Fix broken dependencies.
    

---

## Key Directories

- `/var/lib/dpkg`: Stores `dpkg` metadata.
    
    - `status`: Records the state of installed packages.
        
    - `available`: Lists available packages.
        
- `/etc/dpkg/dpkg.cfg`: Configuration file for `dpkg`.
    

---

## Advanced Tips

### Force Installation

To install a package despite errors (use cautiously):

```
sudo dpkg --force-all -i package_name.deb
```

---

### Debugging Package States

To manually manipulate package states:

Edit `/var/lib/dpkg/status`.

---

`dpkg` is a powerful tool for managing Debian-based systems. While it requires careful use due to its lack of dependency management, it is indispensable for system administrators and advanced users.