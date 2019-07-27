<h1 align="center">macOS Essentials</h1>

<p align="center">Apps and sets that are nice to use on our beatiful system of choice.</p>

## Functions

> An assorted collection of useful macOS Bash-style functions.

#### Get current Wi-Fi password

```bash
wifi_pass() {
    security find-generic-password -D "AirPort network password" -a "$(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}')" -gw
}
```



## [Homebrew](https://brew.sh/)

> Essential package manager for macOS.

Allows you to run `brew cask install <app name>` to install nearly every app you need.

#### Install Homebrew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

---

If you're still wondering dfq for I created this repo — I want to be able to fuck my macBook on the floor right now, buy a new one and return all my settings, a little remembering how and why they are needed.
