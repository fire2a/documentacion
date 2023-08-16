---
layout: default
title: QGIS Cookbook
nav_order: 4
has_toc: false
---

# QGIS Cookbook

1. Install Guides
2. Python scripting
3. Development guides

# Dealing with Windows 💩

## Installing
The easiest wayt to install QGIS is using `winget` (if not available, activate it in MsStore)
1. Open a terminal CMD or Powershell (is recommended to open the administrator mode, because privileges are needed for installing anyway)
2. Type `winget install -e --id OSGeo.QGIS --scope machine` (the scope paramenter is recommended for sharing launchers with other users)
3. Follow onscreen instructions

## python environment
QGIS comes bundled with its own python that's set up in a special way to integrate with all QGIS components such as PyQt, GDAL, GRASS, etc. So activating it is not as simple as running `Scripts/activate.bat`.

### making a environment launcher

{: .info}
To quickly install a python module into QGIS environment, just run `OSGeo4W Shell`

A practical solution seems to copy and modify a `python-qgis.bat` that comes in QGIS bin folder. This file activates the environment and starts python. The goal is to have a location independent launcher that activates the environment and readys the command prompt.

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
2. Select `Python`, properties, sharing... full control for user.

![](./img/qgis_windows_single_user.gif){: width="75%" }
