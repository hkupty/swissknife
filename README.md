# Swissknife

This is a small set of minor scripts that I use to speed up my daily tasks through development.

## Helping

Please, share some scripts and useful tools you have here. This is a very simple and powerful productivity enhancer and every single piece of help might save people tons of hours, spent with repetitive tasks.

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

## Usage
For example, instead of doing:

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

## Modules

Definition of the implemented modules follow below.

### `sd` - Switch Directory
`sd` is a helper script that helps you reach for your project from wherever you are.
You can either give the project an alias or call it for its folder name, whichever option you pleas.

For example, in a directory structure as follows:
```
project/
    awesome-project-1/
    huge-project/
        frontend/
        backend/
```

You can use `sd` withou setting up aliases like this:
```
sd awesome-project-1
sd huge-project
sd huge-project/frontend
sd huge-project/backend
```

Thou this is interesting, `sd` can make use of aliases to make things better:
```
# Aliasing a project
addproj awesome awesome-project-1
sd awesome

# Aliasing a nested folder
addproj hugefront huge-project/frontend
sd hugefront

# Multiple aliases for the same folder work as well
addproj backend huge-project/backend
addproj back huge-project/backend
sd backend
sd back
```
#### TODO
- [ ] Separate `virtualenv` handling from `sd` to allow other kinds of projects (i.e. javascript/nodejs)

### `addproj` - Project aliases
For handling the aliases projects, a `.projcd` file is created at your project root,
which was defined with the variable `TGT_PROJECT_DIR`, when you installed (see Installation).

This module implements two functions for helping you manipulate the aliases:
`addproj` and `delproj`(quite like `alias` and `unalias`), which allow you to make nested project folders easy to react,
for example:
```
addproj new-site incredible-product/frontend/refactoring/version-2/
sd new-site
```

Also, `proj-ls` will output all your aliases:
```
alias                project
[back]               huge-project/backend
[new-site]           incredible-product/frontend/refactoring/version-2/
...
```
### `new-proj` - Project creation
Simply create a new project at `TGT_PROJECT_DIR` by typing:
```
mkproj FOLDER_NAME [ALIAS]
```
It will create a folder, take you there and create a git repo on the folder.

### `bootstrap` - Language setting up
Set up dependencies and structure for your project according to the desired project language.
The intention of this `bootstrap` command is to serve as a frontend for specific language tools with
defaults.
```
bootstrap LANGUAGE_NAME
```
In python, for example, all that is done is the creation of virtualenv and installation of
python dependencies/requirements if a 'requirements.txt' file is found on the current folder.
Other projects might have more complex setting up.

#### TODO
- [ ] Set up more languages:
 - [ ] Javascript (via yeoman)
 - [ ] Javascript (simple node project)
 - [ ] Scala (via g8)
 - [ ] Scala (simple maven structure)
 - [ ] Java (simple maven structure)
 - [ ] Python (3.x)
 - [ ] Python (optional; yeoman-like scaffolding)
- [ ] Create default behaviors for simpler implementation (i.e. deps checking on `_pre_bootstrap`)
- [ ] Allow parameters to be passed and/or variables to be overriden

Currently available languages are:
* Python (virtualenv-2.7/pip)
* Erlang (erlang.mk)

### General TODOs
Some desired goals of this project:
- [ ] Integrate languages with project behaviors (i.e. check for dependency updates once `sd`'ing into a project);
  - [ ] Specially for some languages, such as javascript, start watchers (such as gulp tasks) as `sd`'ing into the project;
  - [ ] Eventually, to support those goals, integrate a bit deeper into the OS by sending desktop notifications for background tasks started this way.
- [ ] Separate repository management from scripts, to allow other backends (such as `hg` or `svn`);
