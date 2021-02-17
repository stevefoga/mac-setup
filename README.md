# mac-setup

This README and associated scripts are information for setting up a mac for my opinionated developer environment. I only do this once every couple years so many things here may go stale between updates. It's mostly a reference.

Last tested 02/05/2021 on the following:

```
MacBook Pro (13-inch, M1, 2021)
Apple M1
macOS Big Sur (11.1)
```
## TODO
- Move to Python 3.9 (ARM support)

## System Preferences

After the initial setup always [install all available updates](https://support.apple.com/guide/mac-help/get-macos-updates-mchlpx1065/mac).

### General

- Set the Appearance to Dark.

### Desktop & Screen Saver

- Set Hot Corners (via Screen Saver) to Bottom-Right -> Launchpad; Bottom-Left -> Desktop.

### Dock & Menu Bar

- Position -> Center
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

### Keyboard

- Key Repeat -> Fastest
- Delay Until Repeat -> Shortest

### Trackpad

- Point & Click
  - Enable Tap to click
  - Click -> Medium
  - Tracking speed -> Fast
  - Enable Force Click and haptic feedback

### Sharing

- Computer Name -> Something Useful (e.g. `stevenfoga-mbp`)

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

`yes | ssh-keygen -t rsa -b 4096 -C "steve.foga@gmail.com" -N "" -f ~/.ssh/id_rsa`

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

#### Installation

1) Make sure Rosetta is installed:  
`softwareupdate --install-rosetta` 

2) Install Homebrew using Rosetta:  
`arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`


### Hack Font

[Hack](https://sourcefoundry.org/hack/) is a great mono-spaced developer font.

```
brew install homebrew/cask-fonts/font-hack
```

### Iterm2

[Iterm2](https://iterm2.com/) is a Terminal replacement for MacOS.

`brew install --cask iterm2`

#### Configuration

- Change hotkey set to Natural Text Editing (Preferences > Profile > Keys > Presets... > Natural Text Editing)

### Rectangle

[Rectangle](https://rectangleapp.com/) is a window manager for mac. It provides keyboard shortcuts for resizing and arranging windows.

`brew install --cask rectangle`

### Sublime Text

[Sublime Text](https://www.sublimetext.com/) is a cross-platform interactive text edior. 

`brew install --cask sublime-text`


#### Configuration

In `Sublime Text > Preferences > Settings`, add:
- `"open_files_in_new_window": false,`  


### Git

#### Configuration

```
git config --global user.name "Steve Foga"
git config --global user.email steve.foga@gmail.com
git config --global username stevefoga
git config --global core.editor vim
git config --global help.autocorect 1
git config --global pull.rebase true
```

### Python (Anaconda)
`brew install --cask anaconda` 

and add to `~/.zshrc`:  
`export PATH="/usr/local/anaconda3/bin:$PATH"` 

### wget
`arch -x86_64 brew install wget` 

### doxygen
`arch -x86_64 brew install doxygen` 




