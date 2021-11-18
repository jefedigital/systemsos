# Packages & Setup

## Security

{% embed url="https://blog.bejarano.io/hardening-macos/" %}

## Package Management

### Homebrew

{% embed url="https://brew.sh" %}

```
$ ruby -e “$(curl -fsSL 
https://raw.githubusercontent.com/Homebrew/install/master/install
)
```

### Cask

`Cask` brings simplicity and speed to installing and managing GUI applications on macOS. In simple terms, it's a way to install applications on your Mac without the hassle of googling it and installing it online.

```
$ brew install cask
```

* List apps: `brew search —- casks`
* Search apps: `brew search (app_name)`
* Install: `brew cask install (app_name)`
* Update: `brew cask upgrade`
* Help: `brew cask help`

## System

### zsh

(already the default shell on MacOS)

`Zsh`, or Z shell, is a Unix shell with appealing colors used as an interactive login shell and command interpreter for shell scripting. Read more about its uses [on GitHub](https://github.com/hmml/awesome-zsh).

```
$ brew install zsh
```

* Setting Zsh as default shell: `chsh -s /bin/zsh`

### tree

`tree` is a tool that lists out the content of directories in a folder in a tree-like format. This useful trick is a life-saver for those who want a quick visual representation of a project’s file structure.

```
$ brew install tree
```

* Run: `tree`

### Rectangle

{% embed url="https://github.com/rxhanson/Rectangle" %}

### Flycut

{% embed url="https://formulae.brew.sh/cask/flycut" %}

### mas

`mas` is a Mac App Store command-line interface that lets you install Mac apps from the App Store directly from the command line.

You can search for apps, install all existing updates, print the version number of an app in the store, and more. There’s even a fun option called lucky that will install the very first search result. Try it if you dare.

```
$ brew install mas
```

* List all apps: `mas list`
* Search for apps: `mas search Xcode`
* Install apps: `mas install 497799835` (the version number of the app)
* Pending update apps: `mas outdated`
* Update apps: `mas upgrade`

## Programming

### git

Create a github [Personal Access Token](https://github.com/settings/tokens) (all Repo permissions, plus read:org) , then install and authenticate with [github-cli](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git):&#x20;

```
brew install gh
gh auth login
```

### miniforge

{% embed url="https://github.com/conda-forge/miniforge" %}

```
brew install miniforge
```

Add to $PATH (/etc/paths)

```
/opt/homebrew/Caskroom/miniforge/base/bin
```

### MySql

instead of using homebrew, install the [MySQL dmg ](https://dev.mysql.com/downloads/mysql/)that installs associated utilities etc.

### MySQL Workbench

```
brew install mysqlworkbench
```

