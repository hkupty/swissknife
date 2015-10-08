# Swissknife

This is a small set of minor scripts that I use to speed up my daily tasks through development.

## Helping

Please, share some scripts and useful tools you have here. This is a very simple and powerful productivity enhancer and every single piece of help might save people tons of hours, spent with repetitive tasks.

## Usage
For exemple, instead of doing:

```shell
cd ~/projects/my-awesome-system-1/
source .venv/bin/activate
# some coding stuff
deactivate

cd ../my-other-great-project/
source .venv/bin/activate
# more coding stuff...
```

I can simply:
```shell
sd awesome
# Start coding

sd great
# Coding again..
```

To do so, all I needed to do once was:
```shell
addproj awesome my-awesome-system-1
addproj great my-other-great-project
```

## Installation

### Installing swissknife
In order to install `swissknife`, all you have to do is run the following command:

```
curl -L https://raw.githubusercontent.com/hkupty/swissknife/master/install-me | bash
```

By default, it installs using the following configs
```bash
# Installation directory
TGT_INSTALL=$HOME/.swissknife/

# Default project folder
TGT_PROJECT_DIR=$HOME/projects/
```

If you want to change the default values, export the variable before calling curl:
```
export TGT_PROJECT_DIR=$HOME/my-projects/this-folder/
curl -L https://raw.githubusercontent.com/hkupty/swissknife/master/install-me | bash
```

### Toggling features
Next, toggle the features you'd like with
```bash
cd ~/.swissknife  # or the folder you installed swissknife
./feature-switch turn-on addproj
./feature-switch turn-on sd
```

### Load scrips
Lastly, source the scripts you turned on:
```bash
# Put this on your bashrc or zshrc
source ~/.swissknife/tools
```
