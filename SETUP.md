# Python Setup and Environment Management

This notebook outlines the setup and usage of Python, covering installation procedures, common integrated development environments (IDEs), and the management of working environments with `Conda` or `venv` and python libraries inside using `conda` or `pip`.

## 1. Python installation

Before using any of these IDEs, you need a working Python installation. Python itself can be installed either through the official [**python.org**](https://www.python.org/) installer or via a distribution such as [**anaconda.com**](https://www.anaconda.com). This installation is independent of the IDE you choose to work in (Sect. 3) — VS Code, Spyder, or Jupyter will all use the same underlying Python interpreter. On HPC systems and JupyterHubs, Python is preinstalled, often with multiple versions or preconfigured environments available for you to load or select.

## 2. Working Environment 

Managing environments is a key part of working with Python, especially when different projects require different versions of packages or even Python itself. An environment is an isolated workspace containing a specific Python interpreter and its installed libraries. This isolation helps avoid version conflicts between projects and ensures reproducibility.

There are two common approaches to environment management in Python:

- **`venv`** – A built-in tool for creating virtual environments (available in any standard Python installation).

- **`Conda`** – A more comprehensive environment and package manager that comes with the Anaconda or Miniconda distribution.

**To create** an environment is to define a new, isolated space for your project. **To activate** the environment is to tell your system (or IDE) to use that specific environment.

Below are examples for both `venv` and `Conda`.

Using `venv`:

```bash
# 1. Create a new environment named 'myenv'
python -m venv myenv

# 2. Activate the environment
myenv\Scripts\activate # (on Windows)

```
Using `Conda`:

```bash
# 1. Create a new environment named 'myenv' with e.g. Python 3.12
conda create -n myenv python=3.12

# 2. Activate the environment
conda activate myenv

```

>Where to run these commands?
>
>You can type these commands into a terminal. The terminal must have access to a Python installation (for `python` and `venv` commands) or a Conda installation (for `conda` commands). If you installed Anaconda or Miniconda, use the Anaconda Prompt, which automatically enables Conda. If you installed Python from python.org use your system terminal where python should be available once installed. On Windows you can use PowerShell or the Eingabeaufforderung (cmd); both work the same for Python installed from python.org. Many IDEs (Sect. 4) also provide graphical tools to create a new Python environment that perform the same steps behind the scenes.

For more detailed information on how to install and manage environments, see the next section 3 – Manage Python Libraries, and the official documentation for [`venv`](https://docs.python.org/3/library/venv.html) and [`Conda`](https://docs.conda.io/projects/conda/en/stable/index.html).

## 3. Manage Python Libraries

Libraries are collections of pre-written code that provide additional functionality to Python. Using them saves time and effort and leveraging existing libraries is considered best practice (or "standard") in modern Python development. Most workflows rely on general-purpose libraries such as `pandas` or `numpy`. Specialized libraries support specific tasks such as data visualization using `matplotlib`. 

When you work in Python, there are two layers to manage. First, the environment tool that defines **where** your code runs (Sect. 2). Second, the package installer that defines **how** libraries get installed **inside** that environment:

- **`pip`** installs libraries from the Python Package Index [PyPI](https://pip.pypa.io/en/stable/user_guide/)
- **`conda`** installs libraries from Conda repositories (e.g. default or `conda-forge`).

<br>

> When to use what?
>
> - Use `conda` when you are working in a Conda environment (created with Anaconda or Miniconda).  
>   Conda can install both Python and non-Python dependencies and is ideal for scientific or research workflows.  
>
> - Use `conda-forge` — a large, community-maintained Conda channel — if a package is not available in the default Conda channel:  
>   ```bash
>   conda install -c conda-forge textblob
>   ```
>
> - Use `pip` if you installed Python directly from python.org or when a package isn’t available through Conda or conda-forge.  
>
> - Inside a Conda environment, it’s fine to mix the two: install what you can with `conda` (or `conda-forge`), then use `pip` for anything that remains unavailable.  
>   Both will install into the active environment.

You can install libraries inside your active environment in several ways:

**Install individual libraries:**

Using pip:

```bash
pip install numpy pandas 
```

Using Conda (Anaconda/Miniconda environments):

```bash
conda install numpy pandas
```

**Install from a list:**

For larger projects, you can use a file — often named requirements.txt (for pip) or environment.yml (for conda) — to list all the libraries your project needs. This makes it easy to reinstall or share your environment.

Example file: `requirements.txt`:
```bash
numpy
pandas
matplolib
```

Then install everything at once:

```bash
pip install -r requirements.txt
```

Most modern IDEs let you install packages **without using the terminal:**

In Jupyter Notebooks (like this one), you simply need to add `!` before the command:

```bash
!pip install numpy
```

## 4. Python Integrated Development Environments (IDEs)

An IDE provides a user interface for writing, running, and debugging Python code. The IDE effectively brings together the **interpreter**, your **environment(s)**, and your **installed packages**. 

When working with Python, you can choose different IDEs such as **Jupyter Notebook**, **VS Code**, **Spyder**, or a **terminal**. 

**Jupyter Notebook is both an application and a file format (`.ipynb`)** that allows interactive coding within documents containing code, text, and outputs. In contrast, **standard Python scripts use the `.py` format**, which contains plain code and can be run in any environment. 

- **[Jupyter](https://jupyter.org)** focuses on interactive, cell-based execution in notebooks (`.ipynb`). This is ideal for experimenting and visualizing code step by step. It also supports Markdown, making it excellent for documentation, which is especially important for sharing code and for teaching.

- **[Spyder](https://www.spyder-ide.org/)** mimics a MATLAB-style IDE, offering script-based coding (`.py`) and a built-in console (also similar to RStudio). 

- **[VS Code](https://code.visualstudio.com/)** is a general-purpose, multi-language IDE that supports both Python scripts (`.py`) AND notebooks (`.ipynb`). It includes extensive extensions and customization options. After installation, add the Python extension to enable `.py` and `.ipynb` file support.

- Running Python scripts (`.py`) from the **terminal** is also common and often essential when executing existing scripts on systems like high-performance computing clusters.

How to get these IDEs? 
- It depends on the IDE! 
- Jupyter Notebook/Lab and Spyder can be installed via pip or conda (e.g., `pip install jupyterlab` / `conda install jupyterlab`, `pip install spyder` / `conda install spyder`).
- With Anaconda Navigator, you can install and launch Jupyter Notebook/Lab and Spyder via the GUI.
- VS Code is not a Python package. It’s a standalone application that you download, install and open separately. After installing, add the Python extension.
- Terminals are already built into your operating system. You can use them to run Python scripts directly once Python is installed.

How to use Python/an environment in these IDEs?
- Two reliable approaches:
    1. Select inside the IDE
    - VS Code: Python: Select Interpreter → pick your env’s interpreter.
    - Jupyter: Select Kernel → pick the kernel that maps to your env.
    - Spyder: Preferences → Python interpreter → choose the env’s interpreter (or install/launch Spyder inside that env).
    2. Activate first, then launch
    - In a terminal: `conda activate myenv` or `source .venv/bin/activate` → start the tool (`jupyter lab`, `spyder`).
- In both cases, code runs and packages install into the chosen environment.

Which IDE to choose?
- Different IDEs have their own built-in (or in VS Code, also extension-based) features to support coding such as tooltips, code completion, debugging, and interactive consoles. These can usually be accessed through buttons, menus, or keyboard shortcuts within each IDE. Therefore, different IDEs fit different preferences and workflows.

## 5. Inside Python Support

Python provides built-in help that you can use directly as you work. For example, try:

```python
help(len)
```

Running this with Python will output:

```
Help on built-in function len in module builtins:

len(obj, /)
    Return the number of items in a container.
```

In IPython/Jupyter you can also view quick documentation using the help operators `?`/`??`. For example:

```python
len?
```

Output:

```
Signature: len(obj, /)
Docstring: Return the number of items in a container.
Type:      builtin_function_or_method
```

Or list your currently defined variables with the IPython magic `%whos`:

```python
x = 1
%whos
```

Output:

```
Variable   Type    Data/Info
----------------------------
x          int     1
```
