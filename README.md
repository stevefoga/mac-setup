# mac-setup

This README and associated scripts are information for setting up a mac for my opinionated developer environment. I only do this once every couple years so many things here may go stale between updates. It's mostly a reference.

Last tested 01/31/2021 on the following:

```
MacBook Pro (13-inch, 2017, Two Thunderbolt 3 ports)
2.3 GHz Dual-Core Intel Core i5
macOS Big Sur (11.1)
```

## System Preferences

After the initial setup the always [install all available updates](https://support.apple.com/guide/mac-help/get-macos-updates-mchlpx1065/mac).

The following are some opinionated [System Preferences]().

### General

- Set the Appearance to Dark.

### Desktop & Screen Saver

- Set Hot Corners (via Screen Saver) to Bottom-Right -> Lock Screen.

### Dock & Menu Bar

- Position -> Left
- Adjust size to be smaller
- Disable magnification
- Enable Automatically Hide & Show Dock
- Battery -> Show Percentage


### Users & Groups

- Disable the Guest account

### Security & Privacy

- General
  - Allow install from App Store & Identified Developers
- FileVault -> Enable
- Firewall -> Enable
  - Block all incoming connections

### Keyboard

- Key Repeat -> Fastest
- Delay Until Repeat -> Shortest
- Modifier Keys (Repeat for all keyboards)
  - Caps Lock -> Control
  - Control -> Control
  - Option -> Option
  - Command -> Command
  - Function -> Function

### Trackpad

- Point & Click
  - Disable "Look up & data detectors"
  - Click -> Medium
  - Tracking speed -> Fast
  - Enable Force Click and haptic feedback

### Sharing

- Computer Name -> Something Useful (e.g. `kpurdon-work`)

### Screenshots

Run the following to put all screenshots in `~/Documents/screenshots`.

```
mkdir ~/Documents/screenshots
defaults write com.apple.screencapture location ~/Documents/screenshots
killall SystemUIServer
```

## Tools & Applications

### XCode Developer Tools

This is basically a requirement for a million things installed on macs, so install it.

`xcode-select --install`

### SSH

- Generate a new SSH key (if `~/.ssh/id_rsa` doesn't exist)

`yes | ssh-keygen -t rsa -b 4096 -C "kylepurdon@gmail.com" -N "" -f ~/.ssh/id_rsa`

- Add the SSH key to the Keychain

`ssh-add -K ~/.ssh/id_rsa`

- Add the SSH key to GitHub

https://github.com/settings/keys

- Update your SSH config by setting `~/.ssh/config` to the following:

```
Host *
 AddKeysToAgent yes
 UseKeychain yes
 IdentityFile ~/.ssh/id_rsa
```

### Homebrew

[Homebrew](https://brew.sh/) is the package manager for MacOS (think apt-get, ...).

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

- Generally prefer installing anything/everything w/ `brew ...` over package installers.

### Hack Font

[Hack](https://sourcefoundry.org/hack/) is a great mono-spaced developer font.

```
brew install homebrew/cask-fonts/font-hack
```

### Iterm2

[Iterm2](https://iterm2.com/) is a Terminal replacement for MacOS.

`brew install --cask iterm2`

#### Configuration

TODO: export current config as file to save/import

### Rectangle

[Rectangle](https://rectangleapp.com/) is a window manager for mac. It provides keyboard shortcuts for resizing and arranging windows.

`brew install --cask rectangle`

### Bash

The version of bash that comes w/ MacOS is often pretty outdated. Install bash from brew and set it as the default shell.

```
brew install bash
echo /usr/local/bin/bash | sudo tee -a /etc/shells
chsh -s /usr/local/bin/bash
```

#### Configuration/Profile

TODO: export current config as a file to save/import

### Git

The version  of git that comes w/ MacOS is often pretty outdated. Install from brew.

```
brew install git
```

#### Configuration

```
git config --global user.name "Kyle Purdon"
git config --global user.email kylepurdon@gmail.com
git config --global username kpurdon
git config --global core.editor emacs
git config --global help.autocorect 1
git config --global pull.rebase true
```

#### GPG Signing

If you use commit signing, follow these instructions.

https://docs.github.com/en/github/authenticating-to-github/signing-commits
https://docs.github.com/en/github/authenticating-to-github/generating-a-new-gpg-key
https://docs.github.com/en/github/authenticating-to-github/telling-git-about-your-signing-key

### Python

The easiest way to manage/install multiple Python version is using [pyenv](https://github.com/pyenv/pyenv). The [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) pieces below are not required but highly reccomended if you use virtualenvs.

#### Before Installing Pyenv

https://github.com/pyenv/pyenv/wiki#suggested-build-environment

`brew install openssl readline sqlite3 xz zlib`

#### Installation

`brew install pyenv pyenv-virtualenv`

Generally this will guide you through the setup, but make sure the following end up in `~/.bash_profile`.

```
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

#### Pyenv Basics

```
pyenv install 3.9.1 # install a specific version
pyenv global 3.9.1  # set the global version to be used in all shells
pyenv shell 3.9.1   # set the version for the active shell
pyenv local 3.9.1   # add a .python-version file to the current directory
```

#### Pyenv Virtualenv Basics

```
pyenv virtualenv 3.9.1 # create a virtualenv
pyenv activate <name>  # activate a virtualenv
pyenv deactivate       # deactivate a virtualenv
```

Of note if a `.python-version` file is present the virtualenv will be automatically activated and deactivated upon entry/exit from that directory.

### Go

`brew install go`

### Chrome

`brew install chrome`

### Gitify

[Gitify](https://www.gitify.io/) is a really handy git notifications app.

`brew install gitify`

### Docker

**Warning** (for M1 see https://docs.docker.com/docker-for-mac/apple-m1/)

`brew install docker`

### Emacs

Install [Emacs for MacOS](https://emacsformacosx.com/) and pull down custom configuration.

```
brew install --cask ispell emacs
pushd $HOME
rm -rf .emacs.d
git clone git@github.com:kpurdon/.emacs.d.git
touch custom.el
popd
```
