# dotfiles

This repo contains scripts to automatically install applications and configure
both the desktop and terminal environment. The two main goals of this repo are:
1. To be able to install a fresh copy of Ubuntu and then simply run a single script to set everything up "the way it was before".
2. To backup configurations and sync them across multiple systems.

NOTE: These dotfiles and scripts have only been tested on Ubuntu 16.04. It is
possible that they no longer work for 14.04 or other versions.

## Folder Structure

I designed the folder structure to be as simple as possible. Since all user
configs reside somewhere under your `$HOME` directory, the `configs/home` folder in
this repo contains all configs relative to the `$HOME` directory. This means a
script can simply loop over all the files found in the `configs/home` folder and know
where to symlink them relative to your `$HOME` directory.

Another benefit is
that you can easily separate private configs (such as your `.ssh/config`) by
simply storing them in another location with the same folder structure (Dropbox
for example). System-specific configs can also be handled by providing a path
based on an assumed unique hostname.
System wide configs are handled the same way. These are stored in the
`configs/root` folder and are symlinked relative to root (`/`).

## Scripts

**configure_desktop.bash**  
Symlinks any configs found in the `configs` folder or any other private folders
you specify. Configuration of Thunderbird, unity and vim is also performed
(Credit for any Vim configs/setup in this repo goes to [chutsu](https://github.com/chutsu/dotfiles)).

**install_apps.bash**  
Automatically installs ubuntu packages and atom plugins as well as some more
complicated custom installs (ROS, chrome).

Use the `-c` flag to indicate only a core installation (core installation
performs a smaller install if time is limited).

Use the `-e` flag to install "entertainment" apps. Basically just a category of
apps that I don't want installed by default on work machines.

Use the `-a` flag to install apps from all categories.

**initialize_system.bash**  
Simply calls the above two scripts. It is meant to be used right after
installing Ubuntu or to update the existing system if any dotfiles or apps
change.

## Using my dotfiles repo

If you want to use this repo for your own dotfiles feel free to fork or copy.
You will most likely want to modify at least the following things although it is
totally optional of course:

- `configs` folder to contain your configs (or just use mine)
- configure_desktop.bash
    - `PRIVATE_CONFIGS_DIR` and `SYSTEM_CONFIGS_DIR` variables to point towards
        your private or system-specific configs directory (or just remove)
    - Any app-specific config functions above the comment line
- install_apps.bash
    - All the `APPS` variables at the very top
    - The `repository_additions` function
    - The `default_install` function to add or remove custom installs
