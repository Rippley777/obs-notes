To install Java and the JDK (Java Development Kit) on your system, follow the instructions for your operating system:

### Windows

1. **Download JDK**:
    
    - Go to the [Oracle JDK download page](https://www.oracle.com/java/technologies/javase-jdk15-downloads.html) or the [OpenJDK download page](https://jdk.java.net/).
    - Download the installer for Windows.
2. **Install JDK**:
    
    - Run the downloaded installer.
    - Follow the instructions to install the JDK. Make sure to note the installation path.
3. **Set Environment Variables**:
    
    - Right-click on "This PC" or "My Computer" and select "Properties".
    - Click on "Advanced system settings" and then "Environment Variables".
    - Under "System Variables", click "New" and add a new variable:
        - Variable name: `JAVA_HOME`
        - Variable value: The path to the JDK installation directory (e.g., `C:\Program Files\Java\jdk-15`).
    - Find the "Path" variable under "System Variables" and click "Edit". Add the following to the end of the value: `;%JAVA_HOME%\bin`
4. **Verify Installation**:
    
    - Open a new Command Prompt and run:        
        `java -version`
        
        This should display the installed Java version.

### macOS

1. **Download JDK**:
    
    - Go to the [Oracle JDK download page](https://www.oracle.com/java/technologies/javase-jdk15-downloads.html) or the [OpenJDK download page](https://jdk.java.net/).
    - Download the macOS installer.
2. **Install JDK**:
    
    - Open the downloaded `.dmg` file and follow the instructions to install the JDK.
3. **Verify Installation**:
    
    - Open a new Terminal window and run:
        
        `java -version`
        
        This should display the installed Java version.

### Ubuntu / Debian-based Linux

1. **Install OpenJDK**:
    
    - Open a terminal and run:
        
        `sudo apt update sudo apt install openjdk-11-jdk`
        
        You can replace `11` with the version number of Java you wish to install.
2. **Set JAVA_HOME (Optional)**:
    
    - Find the installation path of Java:
        
        `sudo update-alternatives --config java`
        
        Note the path of the selected Java version.
    - Open `/etc/environment` in a text editor:
        
        `sudo nano /etc/environment`
        
    - Add the following line, replacing `/path/to/java` with the actual path:
        
        `JAVA_HOME="/path/to/java"`
        
    - Save and exit the editor. Apply the changes:
        `source /etc/environment`
        
3. **Verify Installation**:
    
    - Run:
        `java -version`
        
        This should display the installed Java version.

### CentOS / RHEL-based Linux

1. **Install OpenJDK**:
    
    - Open a terminal and run:
        `sudo yum install java-11-openjdk-devel`
        
        You can replace `11` with the version number of Java you wish to install.
2. **Set JAVA_HOME (Optional)**:
    
    - Find the installation path of Java:
        `sudo update-alternatives --config java`
        
        Note the path of the selected Java version.
    - Open `/etc/environment` in a text editor:
        
        `sudo nano /etc/environment`
        
    - Add the following line, replacing `/path/to/java` with the actual path:
        
        `JAVA_HOME="/path/to/java"`
        
    - Save and exit the editor. Apply the changes:
        `source /etc/environment`
        
3. **Verify Installation**:
    
    - Run:
        `java -version`
        
        This should display the installed Java version.

After following these steps, Java and the JDK should be installed and ready to use on your system.