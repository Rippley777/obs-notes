Linux is a **multi-user operating system**, which means it allows multiple users to use the system concurrently or at different times while maintaining security and resource separation. Here's an overview of the key concepts related to users in Linux:

---

### **1. User Types**

#### **a. Root User**

- The **superuser** with unrestricted access to the system.
- Can perform any action, including system configuration, file access, and user management.
- Identified by the username `root` and has the User ID (UID) of `0`.

#### **b. Regular Users**

- Non-privileged users with access to their own home directories (`/home/username`) and restricted access to system files.
- Can perform day-to-day tasks, like running programs and creating/modifying files within their allowed permissions.

#### **c. System Users**

- Non-login users created by the system or applications for specific purposes (e.g., running services).
- Examples: `www-data` for the web server, `postgres` for the PostgreSQL database.
- Typically have no home directory or shell access.

---

### **2. User Identification**

Each user is identified by:

- **Username**: A human-readable name (e.g., `john`).
- **User ID (UID)**: A numeric identifier for the system (e.g., `1000` for the first user).
- **Group ID (GID)**: Each user belongs to at least one group, used for permissions.

---

### **3. User Management**

#### **User Information Files**

- `/etc/passwd`: Contains user account information (username, UID, home directory, shell, etc.).
- `/etc/shadow`: Stores encrypted user passwords and password policies.
- `/etc/group`: Defines groups and their members.

#### **Commands for User Management**

- [[`adduser`]] / [`useradd`](`adduser`]): Add a new user.
- [[`deluser`]] / `userdel`: Remove a user.
- `passwd`: Change or set a user’s password.
- `usermod`: Modify user properties (e.g., username, group membership).
- `who` / `w`: Show currently logged-in users.

---

### **4. User Directories**

- **Home Directory**: Personal workspace for users (`/home/username`).
- **Root’s Home Directory**: `/root`.

---

### **5. User Permissions**

Linux uses a **permissions model** to manage file and resource access:

- **Owner**: The user who owns the file.
- **Group**: A group of users who can access the file.
- **Others**: Everyone else.

File permissions are represented as: