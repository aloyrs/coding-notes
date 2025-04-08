# Why use virtual environment?

Suppose you have Django version 1.0 already installed on your computer, and you have several projects utilizing it. However, for your latest project, you aim to use Django version 2.0.

To ensure that Django version 2.0 is exclusive to your new project and does not interfere with the existing projects, you opt to create and use a virtual environment (venv) specifically for the new project.

# How to create a venv

In your new project

```bash
python -m venv .venv
```

This command creates a `.venv` folder as a virtual environment.

Activate the virtual environment
(activate everytime you start application):

```bash
.venv/Scripts/activate
```

Now, it's time to configure your Integrated Development Environment (IDE) to use the Python interpreter from your virtual environment.

After configuring the IDE, you can install dependencies for your project within the virtual environment. For example, to install Django:

```bash
python -m pip install django
```

This installs Django specifically within your virtual environment, keeping it isolated from your global Python library.
