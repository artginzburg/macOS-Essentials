<h1 align="center">macOS Essentials</h1>

<p align="center">Apps and sets that are nice to use on our beatiful system of choice.</p>

## Functions

#### Get current Wi-Fi password

```bash
wifipass() {
    security find-generic-password -D "AirPort network password" -a "$(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}')" -gw
}
```


