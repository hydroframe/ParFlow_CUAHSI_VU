# ParFlow_CUAHSI_VU
4 week ParFlow course for CUAHSI Virtual University

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/hydroframe/ParFlow_CUAHSI_VU)

## Running the course in GitHub Codespaces

A Codespace is a computer in the cloud that runs VS Code in your web browser.
This repository's Codespace comes with ParFlow and all of the Python packages
used in class already installed, so you do not need to install anything on
your own computer.  All you need is a GitHub account and a web browser
(Chrome, Edge or Firefox work best).

### 1. Launch a Codespace

1. Sign in to GitHub.
2. Click the **Open in GitHub Codespaces** button above.  Or, on this
   repository's GitHub page, click the green **Code** button, open the
   **Codespaces** tab, and click **Create codespace on main**.
3. Leave the defaults and click **Create codespace**.
4. Wait for the build to finish.  **The first launch is slow**: it compiles
   ParFlow and its libraries from source, which can take 30 minutes or more.
   You can click **View logs** to watch it.  Start it before class, not at
   the start of class.  After the first launch, reopening the same Codespace
   takes under a minute.

When it is ready you will see VS Code in your browser, with the course files
in the **Explorer** panel on the left and a terminal at the bottom.

- **Do your work in the `my_work` folder.**  Git ignores everything in it, so
  your files never get mixed up with the course materials.
- Treat the other course files as read-only, so you can always get the
  newest versions (see below).  To work on a course notebook, copy it into
  `my_work` first: right-click it, choose **Copy**, then right-click
  `my_work` and choose **Paste**.

To get course materials posted after you made your Codespace, open a terminal
(**Terminal > New Terminal** from the ☰ menu) and run:

```bash
cd /workspaces/ParFlow_CUAHSI_VU && git pull
```

This only works if you have not changed the course files, which is why your
own work goes in `my_work`.

### 2. Open a notebook

1. In the **Explorer** panel, click a notebook file (`.ipynb`) to open it.
   To start a new one instead, use the menu (☰, top left):
   **File > New File... > Jupyter Notebook**.
2. Click **Select Kernel** in the top-right corner of the notebook.
3. Choose **Jupyter Kernel...**, then **Python (ParFlow)**.  If it is not in
   the list, choose **Python Environments...** and pick the one in
   `~/.venv`.  It is the same Python.
4. Run a cell with **Shift+Enter**, or run the whole notebook with
   **Run All** at the top.

To check that everything works, run this in a cell:

```python
import os
import parflow
print(os.environ["PARFLOW_DIR"])   # should print /opt/parflow/
```

### 3. Write output as PFB

For now, write ParFlow output as PFB files (ParFlow's own binary format),
not NetCDF.  The ParFlow release in this Codespace has a bug that makes
NetCDF output very slow on Codespaces (ParFlow pull request #779, not yet
released).  PFB is the default, so leave the `NetCDF.*` keys off.  You can
read a PFB file into a NumPy array with:

```python
from parflow.tools.io import read_pfb
pressure = read_pfb("my_run.out.press.00010.pfb")
```

### 4. Save your work and stop the Codespace

- **Your files stay in your Codespace** between sessions, but only there.
  To keep a copy, right-click a file or folder (such as `my_work`) in the
  **Explorer** panel and choose **Download...**.
- **Stop the Codespace when you are done.**  Free GitHub accounts include a
  limited number of Codespace hours each month (students with the
  [GitHub Student Developer Pack](https://education.github.com/pack) get
  more).  A Codespace stops by itself after 30 minutes without activity, but
  stopping it yourself saves hours: go to
  [github.com/codespaces](https://github.com/codespaces), click **...** next
  to your Codespace, and choose **Stop codespace**.
- **To come back**, go to [github.com/codespaces](https://github.com/codespaces)
  and click your Codespace's name.  Do not create a new one each time: a new
  Codespace has to build from scratch again and does not have your files.
- GitHub deletes a Codespace that has not been used for 30 days, along with
  any files in it you have not downloaded.

### What is installed

- ParFlow v3.15.0 (the latest release) with CLM, Hypre, HDF5 and NetCDF,
  installed in `/opt/parflow` (`$PARFLOW_DIR`)
- Python with `pftools`, `subsettools`, `hf_hydrodata`, `numpy`, `pandas`,
  `xarray`, `netCDF4`, `matplotlib`, `bokeh` and Jupyter

The setup is in [`.devcontainer/`](.devcontainer/).
