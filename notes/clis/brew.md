# The `brew` Utility (Mac OS)

[Homebrew](https://brew.sh/) is a command-line utility which makes it easy to install programs on Mac OS.

## Detection

Check to see if Homebrew is installed:

```sh
which brew
```

## Installation

Install Homebrew if necessary:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> FYI: during the installation process you might be asked to also install "Xcode Developer Tools" for the first time if you have not already done so.

## Usage

List installed programs:

```sh
brew list
```

Installing programs:

```sh
brew install my_program # where my_program is the name of the program to be installed
```

Uninstalling programs:

```sh
brew uninstall my_program # where my_program is the name of the program to be installed
```
