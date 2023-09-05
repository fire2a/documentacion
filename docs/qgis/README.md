---
layout: default
title: QGIS cookbook
nav_order: 98
---

# QGIS Cookbook
{: .no_toc}
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# TODO

1. Install Guides
2. Python scripting
3. Development guides

# Plugin Management
## Installation
Plugins can be installed from QGIS official plugin [portal](https://plugins.qgis.org/), from a [custom repo](#adding-a-custom-plugin-repo) server or by [placing a folder](#placing-a-folder) on the proper place.  
QGIS does not handle plugin dependencies, so is up to the user to install them, this is covered extensively for python on [windows](#windows-python-environment) or [linux](#linux-python-environment).

### select and install
1. On QGIS MenuBar: Plugins > Manage and Install Plugins... > All  
2. Type the plugin name
3. Click Install  
An example install is made at the end of [next section](#anchor)

### adding a custom plugin repo
1. On QGIS MenuBar: Plugins > Manage and Install Plugins... > Settings > Add... (button at the bottom right of Plugin Repositories section)  
1. 'Repository details' dialog opens, fill form inputs:  
 Name: any, though "Fire2a" is suggested  
 URL: https://fdobad.github.io/qgis-processingplugin-template/plugins.xml (will change)
1. Confirm (Ok button), repos will be reloaded and a success state should be seen from the fire2a repository

<a name="anchor">
![](./img/install_plugin_server.gif)
</a>

### placing a folder
Download & unzip a release from the repo [releases](https://github.com/fdobad/qgis-processingplugin-template/releases) section  
Example: Unzip `example_plugin_v1.2.3.zip`, inside, a folder named `example_plugin` must be moved to: 
```
# linux (symbolic link it!)
~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/example_plugin
# macos
~/Library/Application Support/QGIS/QGIS3/profiles/default/python/plugins/example_plugin
# windows
%APPDATA%\QGIS\QGIS3\profiles\default\python\plugins\example_plugin
```
Now [select & install](#select-and-install)

## Update
If the plugin is installed via a repo server url, updates will be prompted in QGIS's message bar. Else removing and reinstalling is recommended.
## Remove
If the plugin is installed via a repo server url, removing is easy as pressing uninstall on the plugin's description page. Else the folder must be manually deleted.
NOTE: Removing a repo server url does not remove installed plugins.

# Linux 🗽
## install
* On Debian getting the Long Term Release (LTR) is easy as: 
    * Gnome: `Super (or Meta) Key > type 'QGIS' > Click 'Install' on the Software app dialog`
    * Synaptic: search for qgis, click install
    * Terminal: `sudo apt install qgis qgis-plugin-grass`
    * _Check the following link if you want the latest release instead of stable LTR_
* [Other distributions](https://qgis.org/en/site/forusers/alldownloads.html#linux)

<a id="linux-python-environment"></a>
## python environment

{: .critical}
`sudo pip` is insecure and may break your system!

[_I know all about venvs, take me to the requirements.txt_](#modify)

### create a dedicated venv
To install plugin requirements a virtual environment is the way:
```bash
# recommended: a directory to keep all venvs 
mkdir -p ~/pyenv
# recommended: name this venv qgis
python3 -m venv --system-site-packages ~/pyenv/qgis
```

### activate, launch
must activate venv then run
```bash
$ source ~/pyenv/qgis/bin/activate
(qgis) $ qgis
```

#### handy terminal aliases
```bash
# appending to .bashrc:
echo 'alias pyqgis="source ~/pyenv/qgis/bin/activate"'>>~/.bashrc
echo 'alias myqgis="source ~/pyenv/qgis/bin/activate && qgis"'>>~/.bashrc
# NOTE: must source or open a new shell for aliases to work
$ source ~/.bashrc
$ bash 
# to launch with venv activated
$ myqgis
# to activate venv
$ pyqgis
```

#### activated ~~icon~~ desktop environment launcher

{: .warning}
Although this section is optional, `ModuleNotFoundError`s will rise when starting QGIS from the default launchers, if a plugin with modules not in the systems's python (but on the venv) is active _i.e., ours_

Edit the QGIS ~~icon~~ launcher to activate your venv _(when clicking the icon or using `Open with` over a raster, shp, etc. file)_  
Some DE (xfce, gnome?) allow editing the launcher by 2ndary click on the QGIS icon, then edit; else edit this file `~/.local/share/applications/org.qgis.qgis.desktop`
```
# from
Exec=qgis %F
# to
Exec=bash -c 'source ~/pyenv/qgis/bin/activate && qgis %F'
```

### modify
Most projects include a `requirements.txt` file listing required distributions that provides the needed modules. 
Save link as:
* [Cell2fire plugin requirements](https://raw.githubusercontent.com/fdobad/C2FK/test/requirements.txt)
* [Fire2a toolbox requirements](https://raw.githubusercontent.com/fdobad/qgis-processingplugin-template/main/requirements.txt)  

[_Take me to the tutorial because I don't know what the next commands do_](#python-environment)

```bash
# from activated venv, upgrade tools
(qgis) $ python -m pip install --upgrade pip wheel setuptools
# install (check where you saved it)
(qgis) $ pip install -r ~/Downloads/requirements.txt 
# related bug: matplotlib can't find qt backend
(qgis) $ pip install --upgrade matplotlib
```

[further reading](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)  
<a href="#top">back to top</a>

# MacOS 💰
```zsh
# user plugin folder
~/Library/Application\ Support/QGIS/QGIS3/profiles/default/python/plugins/example_plugin

# QGIS python location
% cd /Applications/QGIS.app/Contents/MacOS/bin

# install into qgis python environment
% ./python3 -m pip install -r ~/Downloads/requirements.txt #  adjust this path
# matplotlib bug: can't find qt_backend
% ./python3 -m pip install --upgrade matplotlib

# make a separate qgis dev environment
% ./python3 -m venv --system-site-packages ~/pyvenv/qgis
```

# Windows 💩™

## installing

{: .warning}
needs administrator privileges  

_TL;DR: browse to [QGIS] until finding the download, then run it_

The easiest way to install QGIS is using `winget` (if not available, activate it in Microsoft Store)
1. Open CMD or Powershell "terminal"  
On your keyboard press the 'Win' button > type 'cmd' > 2dary click on the app > Click 'Run as administrator'
2. Input `winget install -e --id OSGeo.QGIS --scope machine`  
The `--scope machine` option is recommended to making launcher icons for all users
3. Follow on screen instructions (all defaults are ok)

<a id="windows-python-environment"></a>
## python environment

QGIS comes bundled with its own python that's set up in a special way to integrate with all QGIS components such as PyQt, GDAL, GRASS, etc. So activating it is not as simple as running `Scripts/activate.bat`.

### installing requirements

{: .info}
To quickly install a python module into QGIS environment, just open `OSGeo4W Shell` app, then enter `pip install <distribution_name>` or `pip install -r C:\path\to\requirements.txt`

Save link as:
* [Cell2fire plugin requirements](https://raw.githubusercontent.com/fdobad/C2FK/test/requirements.txt)
* [Fire2a toolbox requirements](https://raw.githubusercontent.com/fdobad/qgis-processingplugin-template/main/requirements.txt)  

### making an environment launcher

A practical solution seems to copy and modify a `python-qgis.bat` that comes in QGIS bin folder. This file activates the environment and starts python. The goal is to have a location independent launcher that activates the environment and readys the command prompt. [Save link as](./img/python-qgis-cmd.bat) or:

1. Open `C:\Program Files\QGIS 3.33.3\bin` (check version number)
2. Copy and rename  `python-qgis.bat` to a location of your choosing
3. Edit the 2nd and last line with:
```batch
    REM call it from an absolute path
    REM check version number
    call "%PROGRAMFILES%\QGIS 3.32.1\bin\o4w_env.bat"

    REM print the prefix as check, then leave the command prompt running
    echo python sys says:
    python -c "import sys; print('prefix:', sys.prefix, '\npath:', sys.path)"
    cmd.exe /k
```

![](./img/qgis_windows_activate_venv.gif){: width="75%" }

### make it writable 
Recommended for machines with a single user, or to share modifications to the environment to all users.

1. Open `C:\Program Files\QGIS 3.33.3\apps` (check version number)
2. Select `Python39` (check version), properties, security, ... full control for user.

_After these two steps, you're done!_  
Showing on the gif: After doing step 1 and 2, a success install of qtconsole being installed on `Program Files\Qgis` and not on user's `%APPDATA%` path.

![](./img/qgis_windows_single_user.gif){: width="75%" }

---
[QGIS]: https://qgis.org
