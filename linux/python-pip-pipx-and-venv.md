# Python: pip, pipx, and venv

Notes on managing Python packages and isolated environments on Linux. The core\
idea: **keep project dependencies and command-line tools out of the system**\
**Python.** Modern distros actively discourage installing packages system-wide with\
`pip` - you'll often see an `externally-managed-environment` error if you try -\
because doing so can break system tools that rely on specific package versions.

The right approach splits into two cases: a **virtual environment** for the\
libraries a project imports, and **pipx** for standalone command-line programs.

### The tools at a glance

| Tool   | Use it for                                                                                                                      |
| ------ | ------------------------------------------------------------------------------------------------------------------------------- |
| `pip`  | Installing packages _into the active virtual environment_ for a project.                                                        |
| `venv` | Creating an isolated environment so each project has its own dependencies.                                                      |
| `pipx` | Installing Python **applications/CLI tools** globally, each in its own isolated environment (e.g. `yt-dlp`, `black`, `httpie`). |

The distinction that trips people up: if you're going to `import` it in your own\
code, it belongs in a **venv**; if you're going to _run it as a command_ in your\
terminal, install it with **pipx**.

### Install the necessary tools

```bash
sudo apt install -y python3 python3-pip python3-setuptools python3-venv pipx
```

After installing `pipx`, add its binaries to your `PATH` once:

```bash
pipx ensurepath
```

(Then open a new terminal, or re-`source` your shell config, so the change takes\
effect. See Common Commands > Aliases for how shell config is reloaded.)

### Virtual environments with `venv`

A virtual environment is a self-contained directory with its own Python\
interpreter and its own installed packages, so projects don't interfere with each\
other or with the system Python. It's just a folder - nothing is installed\
globally, and deleting the folder removes the environment completely.

#### Create a virtual environment

```bash
# A shared, general-purpose environment in your home directory:
python3 -m venv ~/.venv

# Or, more commonly, one per project (run from the project folder):
python3 -m venv .venv
```

> Per-project `.venv` folders are the norm. Add `.venv/` to the project's\
> `.gitignore` - you recreate the environment from `requirements.txt`, you don't\
> commit it.

#### Activate the environment

```bash
source ~/.venv/bin/activate
```

Your prompt changes to show the environment name (e.g. `(.venv)`). While it's\
active, `python` and `pip` refer to the environment's copies, and anything you\
`pip install` goes into this environment only.

```bash
pip install requests             # installs into the active venv
pip list                         # see what's installed
pip freeze > requirements.txt    # record exact versions
pip install -r requirements.txt  # recreate them elsewhere
```

That `requirements.txt` workflow is how you reproduce the same environment on\
another machine (or for a teammate): freeze on one side, install from the file on\
the other.

#### Deactivate the environment

```bash
deactivate
```

To delete a venv entirely, deactivate it and remove the directory\
(e.g. `rm -rf .venv` - see the `rm` warning in\
Common Commands > Files and directories).

### Installing CLI tools with `pipx`

Use `pipx` for Python programs you want available everywhere on the system,\
without polluting the global environment or needing `sudo`. Each tool gets its\
own hidden virtual environment, so their dependencies can never conflict - but\
the command itself ends up on your `PATH` like any other.

```bash
pipx install yt-dlp        # install a tool
pipx list                  # see what's installed
pipx upgrade yt-dlp        # upgrade one tool
pipx upgrade-all           # upgrade everything
pipx uninstall yt-dlp      # remove a tool
pipx run cowsay "hi"       # run a tool once without installing it
```

yt-dlp is a good example of a tool that's best installed this way.

### A note on `uv`

[`uv`](https://github.com/astral-sh/uv) is a newer, much faster all-in-one tool\
(written in Rust) that can create virtual environments, install packages, and\
even run tools the way pipx does (`uv tool install …`, `uv venv`, `uv pip …`).\
It's worth knowing about if you work in Python a lot - but `pip`/`venv`/`pipx`\
are built in (or one `apt install` away) and remain the dependable baseline these\
notes assume.
