# Episode 2 — Python and Project Environment

## Overview

This session introduces Python project setup and the tools required to develop and manage Python applications.

Students will learn how Python executes code, how `pip` manages packages, how virtual environments isolate dependencies, and how Git and GitHub support project development.

## Learning Objectives

By the end of this session, students will be able to:

- Understand Python, pip, and virtual environments.
- Check their Python installation.
- Create and activate a virtual environment.
- Install and manage Python packages.
- Use the `colorama` package to display colored terminal output.
- Save and install project dependencies.
- Configure `.gitignore`.
- Publish a Python project to GitHub.

## 1. Overview of the Tools

- **Python:** A programming language used to develop applications and automate tasks.
- **pip:** A tool for installing and managing Python packages.
- **venv:** A Python module for creating isolated virtual environments.
- **Git:** A version control system for tracking changes.
- **GitHub:** A platform for hosting repositories and collaborating.
- **requirements.txt:** A file used to record Python package dependencies.
- **Colorama:** A Python package that makes it easier to display colored text in terminals.

## 2. Check the Python Installation

Open Command Prompt and run:

```bash
python --version
python -m pip --version
```

If Python is not installed, install a supported Python version and ensure it is available from your terminal.

## 3. Create a Python Project

Create a folder named `python-demo`:

```bash
mkdir python-demo
cd python-demo
```

Create a Python file named `main.py`:

```python
print("Hello, Python!")
```

Run the program:

```bash
python main.py
```

Expected output:

```text
Hello, Python!
```

## 4. Create a Virtual Environment

Create an isolated environment for the project:

```bash
python -m venv .venv
```

Activate it on Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

On Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

After activation, the terminal usually displays `(.venv)`.

To deactivate the environment:

```bash
deactivate
```

### Why use a virtual environment?

Different projects may require different versions of the same package. Virtual environments help prevent their dependencies from interfering with each other.

## 5. Install Colorama

With the virtual environment activated, install Colorama:

```bash
python -m pip install colorama
```

Verify the installation:

```bash
python -m pip show colorama
```

List the installed packages:

```bash
python -m pip list
```

## 6. Use Colorama in Python

Update `main.py` with the following code:

```python
from colorama import Fore, Back, Style, init

init(autoreset=True)

print(Fore.GREEN + "Hello, Python!")
print(Fore.RED + "This is an error message.")
print(Fore.YELLOW + "This is a warning message.")

print(Back.BLUE + "This text has a blue background.")

print(Style.BRIGHT + Fore.CYAN + "Welcome to Python Training!")
```

Run the program:

```bash
python main.py
```

The terminal should display messages in different colors and styles.

### Colorama Components

- `Fore`: Changes the text color.
- `Back`: Changes the background color.
- `Style`: Changes text styling, such as brightness and reset behavior.
- `init(autoreset=True)`: Automatically resets formatting after each printed message.

### Common Foreground Colors

```python
Fore.RED
Fore.GREEN
Fore.YELLOW
Fore.BLUE
Fore.MAGENTA
Fore.CYAN
Fore.WHITE
```

### Common Background Colors

```python
Back.RED
Back.GREEN
Back.YELLOW
Back.BLUE
Back.MAGENTA
Back.CYAN
```

### Reset Formatting

```python
print(Fore.RED + "Error!" + Style.RESET_ALL)
print("Normal text")
```

`Style.RESET_ALL` resets the active color and styling.

## 7. Create a Simple Colored Application

Replace `main.py` with this example:

```python
from colorama import Fore, Style, init

init(autoreset=True)

print(Fore.CYAN + "==============================")
print(Fore.CYAN + "     PYTHON TRAINING APP")
print(Fore.CYAN + "==============================")

name = input("Enter your name: ")

print(Fore.GREEN + f"Welcome, {name}!")

age = input("Enter your age: ")

if age.isdigit():
    print(Fore.YELLOW + f"You are {age} years old.")
else:
    print(Fore.RED + "Please enter a valid age.")
```

This example combines package installation with Python input, variables, conditions, and formatted output.

## 8. Manage Dependencies

Save the installed packages to `requirements.txt`:

```bash
python -m pip freeze > requirements.txt
```

The file will contain the installed package versions, including Colorama and any dependencies installed in the environment.

To recreate the environment on another computer:

```bash
python -m pip install -r requirements.txt
```

Run these commands with the project's virtual environment activated.

## 9. Configure .gitignore

Create a `.gitignore` file in the project root:

```gitignore
# Virtual environments
.venv/
venv/

# Python cache
__pycache__/
*.py[cod]

# Environment variables and secrets
.env
.env.*

# Preserve example configuration
!.env.example
```

This prevents common local and temporary files from being tracked by Git.

## 10. Connect the Project to GitHub

Create an empty GitHub repository named `python-demo`.

If your local project has not been initialized with Git, run:

```bash
git init
git add .
git commit -m "Initial Python project with Colorama"
git branch -M main
git remote add origin https://github.com/USERNAME/python-demo.git
git push -u origin main
```

Replace `USERNAME` with your GitHub username.

If you cloned the repository from GitHub at the beginning, do not repeat `git init` or `git remote add origin`.

## 11. Typical Python Project Workflow

1. Open the project folder.
2. Activate the virtual environment.
3. Install dependencies when necessary.
4. Write and run Python code.
5. Update `requirements.txt` when dependencies change.
6. Check changes using `git status`.
7. Commit your changes.
8. Push the commits to GitHub.

## 12. Hands-on Exercise

### Objective

Build a simple Python application that uses Colorama to display colored messages in the terminal.

### Tasks

1. Create a folder named `python-demo`.
2. Create and activate a `.venv` environment.
3. Install the `colorama` package.
4. Create a `main.py` file.
5. Display a welcome message in green.
6. Display a warning message in yellow.
7. Display an error message in red.
8. Ask the user for their name and display a colored greeting.
9. Generate `requirements.txt`.
10. Create a `.gitignore` file.
11. Commit and push the project to GitHub.

### Challenge

Create a simple menu:

1. Display a success message.
2. Display a warning message.
3. Display an error message.
4. Exit the application.

Use different colors for each message and allow the user to select an option.

## 13. Important Notes

- Python executes your source code.
- pip installs and manages packages.
- A virtual environment isolates project dependencies.
- Colorama provides colored terminal output.
- `requirements.txt` helps other developers install the required packages.
- `.gitignore` prevents selected files from being tracked.
- GitHub stores your project remotely; it does not automatically install Python or its dependencies.

## Summary

In this session, students learned how to create a Python project, configure a virtual environment, install and use an external package, manage dependencies, and publish their work to GitHub.

These concepts prepare students for the next session, where they will learn Python programming fundamentals and build more useful applications.