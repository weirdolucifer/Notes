# Steps to Install pyenv and Python

Download Build Dependencies on a System with Internet On a system with internet access (preferably running the same Ubuntu/Debian version):

### Download Required Packages:

First, install apt-offline to make package transfers easier. If apt-offline is not an option, proceed with manual downloads:

1. Create a directory to store the packages:
```
mkdir ~/offline-packages
cd ~/offline-packages
```

2. Use apt to download the .deb files of required dependencies:

```
sudo apt-get install --download-only -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
```
The downloaded .deb files will be located in /var/cache/apt/archives/.


3. Copy the .deb files to the offline-packages directory:
```
cp /var/cache/apt/archives/*.deb ~/offline-packages/
```

### Download pyenv and Plugins

On the same internet-connected machine:

1. Clone the pyenv repository:
```
git clone https://github.com/pyenv/pyenv.git
tar -czvf pyenv.tar.gz pyenv/
```

2. Download pyenv-virtualenv and other plugins:
```
git clone https://github.com/pyenv/pyenv-virtualenv.git
tar -czvf pyenv-virtualenv.tar.gz pyenv-virtualenv/
```

3. Download the Python source (e.g., Python 3.8.10):
```
wget https://www.python.org/ftp/python/3.8.10/Python-3.8.10.tar.xz
```

4. Copy all the following to a USB drive:

offline-packages directory with .deb files
pyenv.tar.gz and pyenv-virtualenv.tar.gz
Python-3.8.10.tar.xz file


### Transfer Files

Copy the files from the USB drive to a local directory:
```
mkdir ~/setup-files
cp -r /path/to/usb/* ~/setup-files/
cd ~/setup-files
```

### Install Build Dependencies

1. Install all .deb files using dpkg:
```
sudo dpkg -i *.deb
```
If you encounter missing dependency errors, re-run the dpkg command until no issues remain.

2. Verify that essential tools are installed:
```
gcc --version
make --version
```


### Install pyenv

1. Extract pyenv:
```
tar -xzvf pyenv.tar.gz -C ~/
```

2. Add pyenv to your shell configuration (~/.bashrc):
```
echo 'export PATH="$HOME/pyenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

3. Reload your shell:
```
exec "$SHELL"
```

4. Verify pyenv installation:
```
pyenv --version
```

### Install pyenv Plugins

1. Extract pyenv-virtualenv:
```
tar -xzvf pyenv-virtualenv.tar.gz -C ~/.pyenv/plugins/
```

2. Verify plugin installation:
```
pyenv virtualenv --version
```

### Install Python Version

1. Copy the Python-3.8.10.tar.xz file to the pyenv source cache:
```
mkdir -p ~/.pyenv/cache/
cp Python-3.8.10.tar.xz ~/.pyenv/cache/
```

2. Install Python 3.8.10:
```
pyenv install -v 3.8.10
```

3. Verify the installation:
```
pyenv versions
```

### Create and Use a Virtual Environment

1. Create a virtual environment:
```
pyenv virtualenv 3.8.10 myproject
```

2. Activate the virtual environment:
```
pyenv activate myproject
```

3. Deactivate the virtual environment:
```
pyenv deactivate
```

### Install Python Packages from requirements.txt

If you have a requirements.txt file, follow these steps:

1. Download the required Python packages on a machine with internet using pip:
```
mkdir ~/offline-pip
pip download -r requirements.txt -d ~/offline-pip
```

2. Transfer the offline-pip directory

3. Install the packages in the virtual environment:
```
cd /path/to/offline-pip/
pip install --no-index --find-links=. -r requirements.txt
```
