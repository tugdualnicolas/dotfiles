# My Win, WSL2, MacOS box auto config

## Windows install via cmd.exe

```bat
rem Allow PowerShell packages to be installed
powershell.exe -c Set-ExecutionPolicy Unrestricted -scope CurrentUser
rem Install scoop
powershell.exe -c "iwr -useb get.scoop.sh | Invoke-Expression"
set PATH=%PATH%;%USERPROFILE%\scoop\shims
rem Install Powershell Core
scoop install 7zip git pwsh sudo
git config --global core.autocrlf input
rem Configure this box; inspect $error if Invoke-Expression fails.
pwsh.exe -c "Invoke-WebRequest -useb https://raw.githubusercontent.com/tugdualnicolas/dotfiles/master/configure.ps1 | Invoke-Expression"
```

Follow instructions for post-configuration.

## WSL

```ps1
sudo powershell.exe -c Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
sudo powershell.exe -c Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
# Restart
curl -LOSs https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
msiexec /i wsl_update_x64.msi
wsl --set-default-version 2
# Install distribution
explorer https://aka.ms/wslstore
```

```sh
sudo apt update
# pyenv build dependencies
sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
printf '. /mnt/c/Users/user/dotfiles/shell-cfg.sh\n' >> ~/.bashrc
printf '#!/bin/sh\n. /mnt/c/Users/user/dotfiles/shell-cfg\n' > ~/.zshrc
printf '[include]\npath = /mnt/c/Users/user/dotfiles/git-cfg.toml\n' > ~/.gitconfig
mkdir -p ~/.config/lsd/
cp /mnt/c/Users/user/dotfiles/.gitattributes ~/.gitattributes
cp /mnt/c/Users/user/dotfiles/lsd.config.yaml ~/.config/lsd/config.yaml
git clone https://github.com/michaeldfallen/git-radar ~/.git-radar
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
git clone https://github.com/pyenv/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
# Reload shell
pyenv install 3.9.5
pyenv global 3.9.5
pip install --upgrade pip
```

## OSX

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/grigoryvp/dotfiles/HEAD/configure_macos.sh)"
# phpenv install 8.0.9 # https://github.com/phpenv/phpenv/issues/90
# phpenv global 8.0.9 # https://github.com/phpenv/phpenv/issues/90
# Install https://macos.telegram.org/
# Install and config Amphetamine autostart and auto session on start and wake.
# mas install 937984704
# Menu: command-drag out "spotlight", "wifi"
# Menu: hammerspoon, amphetamine, command center, time
# Drop "/System/Library/CoreServices/Finder.app" into dock
# Add "gmail" (or use "mimestream"), "google cal", "trello" as chrome apps
# Dock: iTerm2, vscode, browser, Finder, Keepass, Telegram, Mail, Cal, Trello
# In "Preferences/Keyboard/Input Sources":
# * Add "Russian-PC", "Japanese-Romaji"
# In "Preferences/Keyboard/Shortcuts":
# * Remove "input sources" ^-space shortcuts
# * Remove "⇧⌘/" app shortcut
# * Add "⌘W" to "Close Tab" for "Safari" app shortcut
# * Add "⌥⇧⌘V" to "Paste and Match Style" for "Telegram" app shortcut
# In "Preferences/Keyboard/Shortcuts/Mission Control":
# * Add "⇧⌘\" to "Notification Center"
# In "Preferences/Dock & Menu Bar":
# * Remove all icons except 24h clock
# * Enable dock auto-hide
# In "Preferences/Mission Control/Hot Corners" disable quick notes
# Remove all widgets and add notes as widget
# Disable sleep in "Preferences/Energy Saver"
# Disable sound effects in "Preferences/Sound/Effects"
# Enable password lock in "Preferences/Security/General/Require password"
# Configure max "tracking speed" in "Preferences/Trackpad/Point & Click"
# Configure iTerm2 theme, set "JetBrainsMono Nerd Font"
# Configure hammerspoon for autostart
# Configure KeePass
# Configure default email reader in the "Apple Mail" app settings.
# Disable keyboard backlight in the control center
# Intall Xcode (this may take HOURS, better to do with App Store):
# mas install 497799835
# For old macOS versions:
# * Disable welcome screen guest user in "Preferences/Users & Groups"
# * Add 'karabiner_grabber', 'karabiner_observer',
#   'karabiner_console_user_server' into "Accessibility"
# * Install https://d11yldzmag5yn.cloudfront.net/prod/4.4.53909.0617/Zoom.pkg
# * iTunes/Preferences/Devices/Prevent from syncing automatically
```

## Todo

* Ignore subsequent "down" events on buttons that emulate mouse buttons.
* Implement "go-to-background" Ctrl-D via PS keyboard hook.

## License

The following licensing applies to My windows box automatic configuration:
Attribution-NonCommercial-NoDerivatives 4.0 International
(CC BY-NC-ND 4.0). For more information go to
[https://creativecommons.org/licenses/by-nc-nd/4.0/](https://creativecommons.org/licenses/by-nc-nd/4.0/)
