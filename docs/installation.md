## 1. Install the released version ##

<p>
<details open>
<p><summary>via conda / mamba</summary></p>

MintPy is available on the <a href="https://anaconda.org/conda-forge/mintpy">conda-forge</a> channel. The latest released version can be installed via <code>conda</code> as:

```bash
conda install -c conda-forge mintpy
```

or via <code>mamba</code> as:

```bash
mamba install -c conda-forge mintpy
```

</details>

<details>
<p><summary>via docker</summary></p>

Docker allows one to run MintPy in a dedicated container, which is essentially an efficient virtual machine, and to be independent of platform OS. First, install <a href="https://docs.docker.com/install">docker</a> if you have not already done so. Then run the following to pull the latest stable released constainer image version from <a href="https://github.com/insarlab/MintPy/pkgs/container/mintpy">MintPy GitHub Container Registry</a> to your local machine:

```bash
docker pull ghcr.io/insarlab/mintpy:latest
```

<p>Check <a href="./docker.md">docker.md</a> for more details on Docker container image usage, e.g. pulling development version and running in shell or Jupyter server.</p>
</details>

<details>
<p><summary>via apt (Linux Debian)</summary></p>

MintPy is available in the main archive of the <a href="https://tracker.debian.org/pkg/mintpy">Debian</a> GNU/Linux OS. It can be installed by using your favourite package manager or running the following command:

```bash
apt install mintpy
```

The same procedure, in priciple, can be used in <a href="https://ubuntu.com">Ubuntu</a> and all the other <a href="https://wiki.debian.org/Derivatives/Census">Debian derivatives</a>. Check the <a href="https://salsa.debian.org/debian-gis-team/mintpy/-/blob/master/debian/README.Debian">Debian GIS Project</a> page for more detailed usage.
</details>
</p>

## 2. Install the development version ##

Note: The installation note below is tested on Linux and macOS, and is still experimental on Windows (may have bugs).

MintPy is written in Python 3 and relies on several Python modules, check the <a href="https://github.com/insarlab/MintPy/blob/main/requirements.txt">requirements.txt</a> file for details. We recommend using <a href="https://docs.conda.io/en/latest/miniconda.html">conda</a> or <a href="https://www.macports.org/install.php">macports</a> to install the python environment and the prerequisite packages, because of the convenient management and default performance setting with <a href="http://markus-beuckelmann.de/blog/boosting-numpy-blas.html">numpy/scipy</a> and <a href="https://pyresample.readthedocs.io/en/latest/installation.html#using-pykdtree">pyresample</a>.

### 2.1 Install on Linux ###

<p>
<details>
<p><summary>Click to expand for more details</summary></p>

<h4>a. Download source code</h4>

Run the following in your terminal to download the development version of MintPy:

```bash
cd ~/tools
git clone https://github.com/insarlab/MintPy.git
```

<h4>b. Install dependencies via conda</h4>

Install <a href="https://docs.conda.io/en/latest/miniconda.html">miniconda</a> if you have not already done so. You may need to close and restart the shell for changes to take effect.

```bash
# use wget or curl to download in command line or click from the web browser
# for macOS, use Miniconda3-latest-MacOSX-x86_64.sh instead.
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p ~/tools/miniconda3
~/tools/miniconda3/bin/conda init bash
```

Install the dependencies into a custom existing environment [recommended] by running:

```bash
# To create a new custom environment, e.g. named "insar", run "conda create --name insar; conda activate insar"
# To speedup, try "conda install mamba", then use "mamba install" to replace "conda install" below

# Add "gdal'>=3'" below to install extra dependencies if you use ARIA, FRInGE, HyP3 or GMTSAR
# Add "isce2"     below to install extra dependencies if you use ISCE-2
conda install -c conda-forge --file ~/tools/MintPy/requirements.txt
```

<p>
<details>
<p><summary>Or install the dependencies to a new environment, e.g. named "mintpy", by running:</summary></p>

```bash
# Add "gdal'>=3'" below to install extra dependencies if you use ARIA, FRInGE, HyP3 or GMTSAR
# Add "isce2"     below to install extra dependencies if you use ISCE-2
conda create --name mintpy --file ~/tools/MintPy/requirements.txt
conda activate mintpy
```
</details>
</p>

<h4>c. Install MintPy</h4>

<details open>
<p><summary>via pip [recommended]</summary></p>

We recommend installing mintpy in the "editable" mode. This mode installs the package without copying files to your interpreter directory (e.g. the <code>site-packages</code> directory), thus, one could "edit" the source code and have changes take effect immediately without having to rebuild and reinstall.

```bash
python -m pip install -e ~/tools/MintPy
```
</details>

<details>
<p><summary>via path setup</summary></p>

Add below in your source file, e.g. <code>\~/.bash_profile</code> for <em>bash</em> users or <code>\~/.cshrc</code> for <em>csh/tcsh</em> users:

```bash
if [ -z ${PYTHONPATH+x} ]; then export PYTHONPATH=""; fi
export MINTPY_HOME=~/tools/MintPy
export PATH=${PATH}:${MINTPY_HOME}/src/mintpy/cli
export PYTHONPATH=${PYTHONPATH}:${MINTPY_HOME}/src
```
</details>
</details>
</p>

### 2.2 Install on macOS ###

<p>
<details>
<p><summary>Click to expand for more details</summary></p>

<p>Install Xcode with command line tools, if you have not already done so.</p>

<ul>
<li>Install <code>Xcode</code> from App store</li>

<li><p>Install <code>command line tools</code> within XCode and agree to the terms of license.</p></li>

<pre><code>xcode-select --install -s /Applications/Xcode.app/Contents/Developer/
sudo xcodebuild -license</code></pre>

<li>Install <a href="https://www.xquartz.org">XQuartz</a>, then restart the terminal.</li>
</ul>

<p>Install MintPy via conda, which is the same as the <a href="#21-install-on-linux">instruction for Linux</a>.</p>

<p>
<details>
<p><summary>Or install MintPy via MacPorts</summary></p>

Same as the instruction for Linux, except for the "b. Install dependencies" section, which is as below:

Install <a href="https://www.macports.org/install.php">macports</a> if you have not done so. Add the following at the bottom of your <code>~/.bash_profile</code> file:

```bash
# MacPorts Installer addition on 2017-09-02_at_01:27:12: adding an appropriate PATH variable for use with MacPorts.
export PATH=/opt/local/bin:/opt/local/sbin:${PATH}
export MANPATH=/opt/local/share/man:${MANPATH}
# Finished adapting your PATH environment variable for use with MacPorts.
```

Update the port tree with the following command. If your network prevent the use of rsync or svn via http of port tree, try <a href="https://trac.macports.org/wiki/howto/PortTreeTarball">Portfile Sync via a Snapshot Tarball</a>.

```
sudo port selfupdate
```

Install the dependencies by running:

```bash
# install dependencies with macports
# use "port -N install" to use the safe default for prompt questions
sudo port install $(cat MintPy/docs/ports.txt)

# install dependencies not available on macports: pysolid, pykml, pykdtree, pyresample, cdsapi
sudo -H /opt/local/bin/pip install git+https://github.com/insarlab/PySolid.git
sudo -H /opt/local/bin/pip install git+https://github.com/insarlab/PyAPS.git
sudo -H /opt/local/bin/pip install git+https://github.com/tylere/pykml.git
sudo -H /opt/local/bin/pip install git+https://github.com/storpipfugl/pykdtree.git
sudo -H /opt/local/bin/pip install git+https://github.com/pytroll/pyresample.git
sudo -H /opt/local/bin/pip install git+https://github.com/ecmwf/cdsapi.git
```
</details>
</details>
</p>
</p>

### 2.3 Install on Windows ###

<p>
<details>
<p><summary>Click to expand for more details</summary></p>

Same as the <a href="#21-install-on-linux">instruction for Linux</a>, except for the "c. Install MintPy" section, only the <code>pip install</code> approaches are recommended, as the <code>path setup</code> approach is not tested.
</details>
</p>

## 3. Post-Installation Setup ##

#### a. ERA5 for tropospheric correction ####

Set up an account for ERA5 to download weather re-analysis datasets for tropospheric delay correction as described in <a href="https://github.com/insarlab/pyaps#2-account-setup-for-era5">insarlab/PyAPS</a>.

<code>WEATHER_DIR</code>: Optionally, if you defined an environment variable named <code>WEATHER_DIR</code> to contain the path to a directory, MintPy will download the GAM files into the indicated directory. Also, MintPy will look for the GAM files in the directory before downloading a new one to prevent downloading multiple copies if you work with different dataset that cover the same date/time.

#### b. Dask for parallel processing ####

We recommend setting the <code>temporary-directory</code> in your <a href="https://docs.dask.org/en/stable/configuration.html">Dask configuration file</a>, e.g. <code>~/.config/dask/dask.yaml</code>, by adding the following line, to avoid the potential <a href="https://github.com/insarlab/MintPy/issues/725">workspace lock issue</a>. Check the <a href="./dask.md">dask.md</a> file for more details on parallel processing.

```yaml
temporary-directory: /tmp  # Directory for local disk like /tmp, /scratch, or /local

# If you are sharing the same machine with others, use the following instead to avoid permission issues with others.
# temporary-directory: /tmp/{replace_this_with_your_user_name}
```

#### c. Extra environment variables setup ####

We recommend setting the following environment variables, e.g. in your <code>~/.bash_profile</code> file, to avoid occasional errors with GDAL VRT and HDF5 files I/O.

```bash
export VRT_SHARED_SOURCE=0             # do not share dataset while using GDAL VRT in a multi-threading environment
export HDF5_DISABLE_VERSION_CHECK=2    # supress the HDF5 version warning message (0 for abort; 1/2 for printout/suppress warning message)
export HDF5_USE_FILE_LOCKING=FALSE     # request that HDF5 file locks should NOT be used
```
