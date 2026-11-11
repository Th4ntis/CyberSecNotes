# Linux General

My notes on the Linux operating system - day-to-day commands, configuration, and the tools I reach for most. They're written for my own setup but should make sense to anyone getting comfortable on the command line. I personally use [Debian](https://www.debian.org/) with the KDE Plasma desktop environment instead of the default GNOME. It's lightweight, highly customizable, and in my experience just works with little to no trouble. Everything in these notes that mentions `apt` applies to it directly.

### Map of these notes

Start here and branch out. Each note stands on its own, but they're cross-linked\
where topics overlap.

| Note                 | What it covers                                                                                             |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| Common Commands      | The everyday toolkit: files, navigation, redirection, networking, services, package managers, and aliases. |
| Permissions and sudo | The Linux permission model (`chmod`, `chown`) and running commands as root with `sudo`.                    |
| SED, AWK, and Grep   | Searching and transforming text - the three classic tools that power most shell pipelines.                 |
| Python Pip Pipx Venv | Managing Python packages cleanly with `venv`, `pip`, and `pipx`.                                           |
| TMUX                 | Terminal multiplexing: persistent sessions, windows, and panes (plus my full config).                      |
| QEMU - Virt-Manager  | Virtual machines with QEMU/KVM and the Virt-Manager GUI.                                                   |
| YT-DLP               | Downloading audio and video from the command line.                                                         |

### What is a Linux "distro"?

A **distribution** (distro) is a complete operating system built around the Linux kernel, bundled with a package manager, default applications, and usually a desktop environment. Distros differ mainly in three things:

* **Package manager** - how you install and update software (`apt`, `dnf`,\
  `pacman`, …). See Common Commands > Installing / updating / upgrading.
* **Release model** - a _fixed release_ ships versioned snapshots every so often\
  (Ubuntu, Debian, Fedora), while a _rolling release_ continuously updates to the\
  latest of everything (Arch).
* **Default software** - the desktop environment, pre-installed apps, and\
  configuration choices.

The underlying kernel and the core command-line tools are essentially the same across all of them, which is why the skills in these notes transfer between distros.

### Popular Linux distros (in no particular order)

| Distro                            | Family        | Package manager | Notes                                                                                      |
| --------------------------------- | ------------- | --------------- | ------------------------------------------------------------------------------------------ |
| [Ubuntu](https://ubuntu.com/)     | Debian        | `apt`           | Beginner-friendly, huge community, long-term-support releases.                             |
| [Mint](https://linuxmint.com/)    | Debian/Ubuntu | `apt`           | Polished and familiar; a great first Linux.                                                |
| [Debian](https://www.debian.org/) | Debian        | `apt`           | Rock-solid and conservative; the base for Ubuntu and many others.                          |
| [Fedora](https://getfedora.org/)  | RHEL          | `dnf`           | Modern and close to upstream; where many new features land first.                          |
| [Arch](https://archlinux.org/)    | Arch          | `pacman`        | Rolling release, build-it-yourself, with an excellent [wiki](https://wiki.archlinux.org/). |
| [Manjaro](https://manjaro.org/)   | Arch          | `pacman`        | Arch made more approachable, with sane defaults.                                           |

Package-manager basics for each family are inCommon Commands > Installing / updating / upgrading.

### Desktop environments vs. window managers

How your desktop looks and behaves is largely decided by one choice:

* A **Desktop Environment (DE)** - KDE Plasma, GNOME, XFCE - is a complete, integrated desktop: panels, a file manager, a settings app, and a consistent look, all working together out of the box.
* A **Window Manager (WM)** - i3, bspwm, awesome - _only_ manages where windows go. It's far more lightweight and keyboard-driven, but you assemble the rest of the desktop (bar, launcher, notifications, wallpaper) yourself.

I find [KDE](https://kde.org/) and [XFCE](https://xfce.org/) the most customizable with the least effort. On KDE you can even add tiling-WM behavior with something like [Krohnkite](https://github.com/esjeon/krohnkite) instead of committing to a full WM. WMs such as [i3](https://i3wm.org/),\
[bspwm](https://github.com/baskerville/bspwm), and [awesome](https://awesomewm.org/) are great once configured - just expect to spend time on it, and back up your configs often (see Dotfiles).

### Dotfiles

User-specific application configuration is traditionally stored in **dotfiles** - files whose names start with a dot (e.g. `.zshrc`, `.vimrc`, `.tmux.conf`). The leading dot hides them from a normal `ls`, so use `ls -a` to see them (more in Common Commands > Files and directories).

It's a good idea to track your dotfiles with a version-control system such as Git. That gives you a history of changes, an easy way to roll back a mistake, and a way to synchronize the same setup across machines (and a backup if a machine dies). Most people version at least their shell config, editor config, and tmux config.

My dotfiles live [on my GitHub](https://github.com/Th4ntis/dotfiles). There are plenty of other [dotfile projects](https://github.com/topics/dotfiles) for inspiration, and tools like [GNU Stow](https://www.gnu.org/software/stow/) or [chezmoi](https://www.chezmoi.io/) help manage symlinking them into place so the files can live in one tracked folder while appearing where each app expects them.

### Ricing

"Ricing" is the hobby of customizing your system to improve how it looks or works - configuring applications, picking a color scheme, and refining your workflow until it fits you. In my opinion, ricing should start with your **desktop environment or window manager**, since that sets the foundation everything else builds on. The [r/unixporn subreddit](https://www.reddit.com/r/unixporn/) is a great place to find ideas and see what's possible, and most setups you'll admire there are driven entirely by dotfiles you can study and adapt.
