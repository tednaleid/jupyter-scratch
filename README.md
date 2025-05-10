# VSCode Setup/Installation

I'm using VSCode's python, jupyter plugins to run notebooks locally:

* https://marketplace.visualstudio.com/items?itemName=ms-python.python
* https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter
* https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter-keymap

(the keymap plugin should be installed with Jupyter, but I've had issues with this, so confirm it is there)


# Python Setup and Kernel Installation

We use [uv](https://github.com/astral-sh/uv?tab=readme-ov-file#installation) to manage Python and virtual environments.

Install `uv`:

```
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## If you want to create a new directory/project rather than using this repo

Create a new project (creates the `myproject` directory):

```
uv init myproject
cd myproject
uv add ipykernel jupyterlab
source .venv/bin/activate
```

If you're using an existing directory (or a clone of this repo) that has a `pyproject.toml`, you can install dependencies using:

```bash
uv sync
```

If you're in a VSCode terminal, you'll want to restart it after running `uv sync` to pick up the new virtual environment.

It should have the directory prefix added to the prompt.


# Installing Dependencies in a New Project

These should be installed in a clone of this repo, but if you've created a new directory/project, you can add the various kernels and tools using these instructions.


## Python linting and deependencies

Add dependencies (they'll get put into your `pyproject.toml` file), this implicitly creates a `.venv` in the local directory:
```
uv add ruff
```

And run them:
```
uv run ruff
```

## Jupyter Notebook/Kernel Setup

To run a Jupyter Labs instance to run Jupyter Notebooks, you can run:

```bash
uv add ipykernel
uv add jupyterlab
```

And run it:

```bash
jupyter-lab
```

This should open a new window in your browser with Jupyter Labs.

### To Create a notebook

You can create a new file with an `.ipynb` extension, or press ctrl-cmd-opt-N to bring up the "New" menu.



### To add a Bash kernel

```bash
uv add bash-kernel
uv run -m bash_kernel.install          
```

In the upper right, click on the kernel, choose "Select Another Kernel" -> "Jupyter Kernel" -> "Bash".

### To add a TypeScript Deno 2.0 Kernel

```bash
brew install deno
deno jupyter
```

In the upper right, click on the kernel, choose "Select Another Kernel" -> "Jupyter Kernel" -> "Deno".


### To install a Kotlin kernel

```bash
uv add kotlin-jupyter-kernel
```

You might need to run this to [fix the location of the kernel spec](https://github.com/Kotlin/kotlin-jupyter?tab=readme-ov-file#troubleshoot-your-installation):

```bash
uv run -m kotlin_kernel fix-kernelspec-location
```

You'll likely need to shut down VSCode and restart it for the kernel to appear.

It should be called `Kotlin (.venv) /python`