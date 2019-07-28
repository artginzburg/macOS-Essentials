<h1 align="center">macOS Essentials</h1>

<p align="center">Apps and sets that are nice to use on our beatiful system of choice.</p>

## Functions

> An assorted collection of useful macOS Bash-style functions.

### Get current Wi-Fi password

```powershell
ssid() {
	/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}'
}
wifi_pass() {
	if [ "$1" == "copy" ]
	then	
		wifi_pass | tr -d '\n' | pbcopy
	else
		security find-generic-password -D "AirPort network password" -a "$(ssid)" -gw
	fi
}
```

Now you could run `wifi_pass`, maybe adding ` copy` to get the result to your clipboard



With [Homebrew](#Homebrew) installed, you can extend `wifi_pass` function to make a QR code that can be scanned using mobile phone to join your network:

Just `brew install qrencode` and

```powershell
wifi_qr() {
    qrencode -o Desktop/wifi.png -s 20 -m 3 "WIFI:S:$(ssid);T:WPA;P:$(wifi_pass);;"
}
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



## [Homebrew](https://brew.sh/)

> Essential package manager for macOS.

Allows you to run `brew cask install <app name>` to install nearly every app you need.

#### Install Homebrew

```powershell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
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
