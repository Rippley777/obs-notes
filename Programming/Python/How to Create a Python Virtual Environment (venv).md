

A **Python virtual environment (venv)** allows you to create an isolated workspace for your Python projects, ensuring dependencies do not interfere with system-wide packages.

## **1. Check if Python is Installed**

Ensure Python is installed on your system by running:

```sh
python --version
```

or (for Python 3 specifically):

```sh
python3 --version
```

If Python is not installed, download and install it from [python.org](https://www.python.org/).

## **2. Create a Virtual Environment**

Navigate to your project directory and create a virtual environment by running:

```sh
python -m venv venv
```

or (if using Python 3):

```sh
python3 -m venv venv
```

This will create a folder named `venv` containing the virtual environment.

## **3. Activate the Virtual Environment**

### **Windows:**

```sh
venv\Scripts\activate
```

### **Mac/Linux:**

```sh
source venv/bin/activate
```

Once activated, you should see `(venv)` in your terminal prompt.

## **4. Installing Dependencies**

After activation, install packages using `pip`:

```sh
pip install package_name
```

To save installed packages:

```sh
pip freeze > requirements.txt
```

To install dependencies from a file:

```sh
pip install -r requirements.txt
```

## **5. Deactivate the Virtual Environment**

To exit the virtual environment, simply run:

```sh
deactivate
```

---

Using virtual environments helps keep projects organized and dependencies managed efficiently. 🚀