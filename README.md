<h1 align="center">macOS Essentials</h1>
<p align="center">Apps and sets that are nice to use on our beatiful system of choice.</p>

## Applications

Most of them are the newest and most convenient applications, replacing the already outdated ones.

### Productivity

#### [Maccy](https://github.com/p0deje/Maccy) - clipboard manager

- Keeps the history of what you copy and lets you easily navigate, search and use previous clipboard contents.

![Maccy.app](https://github.com/p0deje/Maccy/raw/master/Maccy/Assets.xcassets/Demo.dataset/demo.gif)

- It has wonderful <kbd>⌘</kbd>+<kbd>⇧</kbd>+<kbd>C</kbd> shortcut, but I changed it to <kbd>⌥</kbd>+<kbd>⇧</kbd>+<kbd>C</kbd> because the initial option is used in many other applications.

## Command Line tools

### [Homebrew](https://brew.sh/)

> Essential package manager for macOS.

Allows you to run `brew install <package>` and `brew cask install <app>` to install nearly everything you need.

#### Install Homebrew

```powershell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Packages

> Remember, just `brew install <package>` — 3 seconds for the magic to appear!

- [youtube-dl](https://github.com/rg3/youtube-dl) - Download media from YouTube and other video sites.

- [thefuck](https://github.com/nvbn/thefuck) - Corrects errors in previous console commands.

    ```powershell
    $ puthon
    No command 'puthon' found
    $ fuck
    Python 3.4.2 (default, Oct  8 2014, 13:08:17)
    ```

- [qrencode](https://fukuchi.org/works/qrencode/index.html.en) - Accepts a string or a list of data chunks then encodes in a QR Code symbol as a bitmap array.

### Functions

> An assorted collection of useful macOS Bash-style functions.

#### Get current Wi-Fi password

    run `wifi_pass`, maybe adding ` -c` to get the result to your clipboard

```powershell
ssid() {
    /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}'
}
wifi-pass() {
  local ssid=$(ssid)
  if [ "$1" != "" ]; then
    case $1 in
      -c | --copy )
        if [ "$2" != "" ]; then
          wifi-pass $2 | tr -d '\n' | pbcopy
        else
          wifi-pass -c $ssid
        fi
      ;;
      -qr | --qrencode )
        if [ "$2" != "" ]; then
          qrencode -o ~/Desktop/$2.png -s 20 -m 3 "WIFI:S:$2;T:WPA;P:$(wifi-pass $2);;"
        else
          wifi-pass -qr $ssid
        fi
      ;;
      * )
        security find-generic-password -D "AirPort network password" -a "$1" -gw
    esac
  else
    wifi-pass $ssid
  fi
}
```

With [qrencode](#Packages) package installed, you can extend the `wifi-pass` function to make a QR code that can be scanned using a mobile phone to join your network:

```powershell
wifi-pass -qr <ssid>
```

### Profiling functions

> Use this to quickly enable new settings you get on the web

```bash
edit() {
    open .bash_profile
}
reload() {
    . .bash_profile
}
```

## Printing

#### Clear Print Queue

```bash
cancel -a -
```

#### Quit Printer App After Print Jobs Complete

```powershell
defaults write com.apple.print.PrintingPrefs "Quit When Finished" -bool true
```

## System

##### Set Login Window text

```powershell
sudo defaults write /Library/Preferences/com.apple.loginwindow LoginwindowText "Can't touch this..."
```

---

If you're still wondering dfq for I created this repo — I want to be able to fuck my MacBook on the floor right now, buy a new one and return all my settings, a little remembering how and why they are needed.
