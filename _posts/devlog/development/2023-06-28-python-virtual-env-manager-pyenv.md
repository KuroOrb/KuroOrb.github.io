---
layout: post
title: "Installation and Usage of Pyenv and Pyenv Virtualenv"
subtitle: "Python Version Manager Coupled with Virtual Environment Manager"
category: devlog
tags: development terminal python bash zsh virtualenv pyenv
---

Python is a very popular language with multiple use cases ranging from web development with tools such as Flash and Django to heavier computational work in the area of machine learning and AI.

When using a language such as Python, you will find yourself running in to dependency issues when working on various projects. This could be that the current code base only works with Python2 and not Python3, or it could be a case that a package was changed or phased out such as the changes made when Python3.9 updated to Python3.10. These issues are annoying to fix and are very time consuming when trying to trouble shoot.

The solution to this issue is the use of a Python Version Manager in pair with a Virtual Environment manager. Over the few years I have spent using Python, I have found that [Pyenv](https://github.com/pyenv/pyenv) is one of the best python version managers out there. This is due mostly to its simple commands and ease of use. This tool alone does not come with a virtual environment manager, but it does support plugins. That is where the virtual environment manager, [Pyenv-Virtualenv](https://github.com/pyenv/pyenv-virtualenv) comes into play.

In this blog I will show you how to set up Pyenv and Pyenv-Virtualenv in a BASH shell environment as well as a ZSH shell environment. BASH set-up aims for development environments that are using WSL2 or a base OS/VM such as Ubuntu. ZSH set-up aims for development environments that are using OSX or if there was a switch to ZSH.

Once we get this tool installed and working, I will present some of the most common commands that you will most likely use when setting up a python development environment with Pyenv.

## Prerequisite

* `bash`
* `zsh`
* `git`

## Initial Installation of Pyenv

For linux environments the install command is as follows:
```shell
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

Optionally, an alternative install method for macOS is as follows:
```shell
brew update
brew install pyenv
```

---

## Shell Dependent Configurations

The source files we will update can be found in your specific user's home directory. Check your shell and for the shell source files using the following commands.

```shell
# Check for Shell
echo $SHELL

# Check for Files
cd ~
ls -la
```

### BASH

**.bashrc**
For the first step, the following commands can be copy and pasted so that your `~/.bashrc` file can be updated accordingly.

```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```

Next, depending on the linux distribution, the bash profile file might vary. This is where you would need to choose the section that pertains to your specific profile file name.

**.profile**
```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
```

**.bash_profile**
```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
```

If neither of these profile files are listed in your home directory, then create your own `.profile` file. If a files exists but the name is not listed above, then change the specified path within the command to work with your profile file's name.

### ZSH
Similar to BASH you will add the following commands to your `.zshrc` file.

**.zshrc**
```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## Testing Pyenv

Now that we have properly installed Pyenv, we need to restart our shell so that our modified source files can initialize Pyenv. To do this, use the following command:

```shell
exec "$SHELL"
```

Lastly, to test that everything was installed properly, we will run the command that lists out all the possible Python versions that we can install. The command is as follows:

```shell
pyenv install -l
```

If there was no error, then you have successfully installed Pyenv and can move on to install Pyenv-Virtualenv. Otherwise, go back through these steps or check out the [Pyenv github repository](https://github.com/pyenv/pyenv) for more information.

---

## Installation of Pyenv-Virtualenv

Once Pyenv is installed and working, the set-up for Pyenv-virtualenv is very trivial. This can be done with the following command:

```shell
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
```

If you went the Brew route on macOS, then you can use the following command for installing the plugin and once done, continue with the next step.

```shell
brew install pyenv-virtualenv
```

In addition, there is an optional feature of enabling auto-activation of your virtualenvs. I find this useful so I recommend adding this. This can be done with the following command:

**For BASH**
```shell
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

**For ZSH**
```shell
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

## Testing Pyenv-Virtualenv

Now that we have properly installed Pyenv-Virtualenv, we need to restart our shell so that our modified source files can initialize the plugin. To do this, use the following command:

```shell
exec "$SHELL"
```

Lastly, for testing if this plugin was set-up properly, we will run the following command that lists all of our current virtual environments.

```shell
pyenv virtualenvs
```

If there was no error, you can move on to some of the most common commands that I find helpful when setting up my python environment with this tool. Otherwise, re-read the steps given above or check out the [Pyenv-Virtualenv github repository](https://github.com/pyenv/pyenv-virtualenv) for more information.

---

## Most Common Commands for Managing Pyenv and Pyenv-Virtualenvs

For sake of simplicity and getting straight to the point, I will just add all of these commands into one big code block with comments noting one they do.

### PYENV

```shell
# List Python Versions
pyenv install -l

# Install Specific Version
pyenv install [VERSION]

# List Installed Versions
pyenv versions

# Select Version for Shell Session
pyenv shell [VERSION]

# Auto Activate Version (when switched to specific directory/sub-directory, must use command in target directory)
pyenv local [VERSION]

# Set Global Version for User Account
pyenv global [VERSION]
```

### PYENV-VIRTUALENV

```shell
# Create Virtualenv
pyenv virtualenv [VERSION] [NAME]

# List Virtualenvs
pyenv virtualenvs

# Activate Virtualenv
pyenv activate [NAME]

# Deactivate Virtualenv
pyenv deactivate

# Delete Virtualenv
pyenv virtualenv-delete [NAME]
```

This wraps up my notes on setting up a Python Version manager and Virtual Enviromnet manager using Pyenv and Pyenv-Virtualenv.