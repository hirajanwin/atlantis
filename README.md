![Atlantis: Debug iOS with ease](https://raw.githubusercontent.com/ProxymanApp/atlantis/main/images/cover.png)

A little and powerful iOS framework for intercepting HTTP/HTTPS Traffic from your app. No more messing around with proxy, certificate config. 

[![Version](https://img.shields.io/cocoapods/v/atlantis-proxyman.svg?style=flat)](https://cocoapods.org/pods/atlantis-proxyman)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Platform](https://img.shields.io/cocoapods/p/atlantis-proxyman.svg?style=flat)](https://cocoapods.org/pods/atlantis-proxyman)
[![Twitter](https://img.shields.io/twitter/url?label=%40proxyman_app&style=social&url=https%3A%2F%2Ftwitter.com%2Fproxyman_app)](https://twitter.com/proxyman_app)
[![Join the chat at https://gitter.im/Proxyman-app/community](https://badges.gitter.im/Proxyman-app/community.svg)](https://gitter.im/Proxyman-app/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![License](https://img.shields.io/cocoapods/l/atlantis-proxyman.svg?style=flat)](https://cocoapods.org/pods/atlantis-proxyman)

## Features
- [x] **Automatically** intercept all HTTP/HTTPS Traffic with ease
- [x] ✅ **No need to config HTTP Proxy, Install or Trust any Certificate**
- [x] Support iOS Physical Devices and Simulators
- [x] Review traffic log from [Proxyman](https://proxyman.io)
- [x] Categorize the log by project and devices.
- [x] Only for Traffic Inspector, not for Debugging Tools
- [x] Ready for Production

![Atlantis: Debug iOS with ease](https://raw.githubusercontent.com/ProxymanApp/atlantis/main/images/proxyman_atlantis_3.png)

## How to use
1. Install Atlantis by CocoaPod or SPM, then starting Atlantis
```swift
import Atlantis

// Add to the end of `application(_:didFinishLaunchingWithOptions:)` in AppDelegate.swift or SceneDelegate.swift
Atlantis.start()
```

2. Make sure your iOS devices/simulator and macOS Proxyman are in the same Wifi Network or connect your iOS Devices to Mac by USB cables
3. Open macOS [Proxyman](https://proxyman.io) (or [download the lasted here](https://proxyman.io/release/osx/Proxyman_latest.dmg)) (2.11.0+)
4. Open your iOS app and Inspect traffic logs from Proxyman app
5. Enjoy debugging ❤️

## Requirement
- macOS Proxyman app 2.11.0+
- iOS 12.0+ / macOS 10.12+
- Xcode 11+
- Swift 5.0+

### Required Configuration for iOS 14+
From iOS 14, it's required to add `NSLocalNetworkUsageDescription` and `NSBonjourServices` to your info.plist
- Open Info.plist file and adding the following keys and values:

```xml
<key>NSLocalNetworkUsageDescription</key>
<string>Atlantis would use Bonjour Service to discover Proxyman app from your local network.</string>
<key>NSBonjourServices</key>
<array>
    <string>_Proxyman._tcp</string>
</array>
```

## Install
### CocoaPod
- Add the following line to your Podfile
```bash 
pod 'atlantis-proxyman'
```

### Swift Packages Manager
- Add `https://github.com/ProxymanApp/atlantis` to your project by: Open Xcode -> File Menu -> Swift Packages -> Add Package Dependency...

### Carthage
1. Add to your Cartfile
```
github "ProxymanApp/atlantis"
```
2. Run `carthage update`
3. Drag Atlantis.framework from your project
3. Create a Carthage Script as the [Carthage guideline](https://github.com/Carthage/Carthage#quick-start)  

For Carthage with Xcode 12, please check out the workaround: https://github.com/Carthage/Carthage/blob/master/Documentation/Xcode12Workaround.md

## FAQ
#### 1. How does Atlantis work?

Atlantis uses [Method Swizzling](https://nshipster.com/method-swizzling/) technique to swizzle certain functions of NSURLSession and NSURLConnection that enables Atlantis captures HTTP/HTTPS traffic on the fly.

Then it sends to [Proxyman app](https://proxyman.io) for inspecting later.

#### 2. How can Atlantis stream the data to the Proxyman app?

As soon as your iOS app (Atlantis is enabled) and the Proxyman macOS app are the same **local network**, Atlantis could discover the Proxyman app by using [Bonjour Service](https://developer.apple.com/bonjour/). After the connection is established, Atlantis will send the data via Socket.

#### 3. Is it safe to send my network traffic logs to the Proxyman app?

It's completely **safe** since your data is locally transferred between your iOS app and the Proxyman app, no Internet is required. All traffic logs are captures and send to the Proxyman app for inspecting on the fly. 

Atlantis and Proxyman app do not store any of your data on any server.

#### 4. What kind of data that Atlantis capture?

- All HTTP/HTTPS traffic from your iOS apps, that integrate the Atlantis framework 
- Your iOS app name, bundle identifier, and small size of the logo
- iOS devices/simulators name and device models.

**All the above data are not stored anywhere (except in the memory)**. It will be wiped out as soon as you close the app. 

They are required to categorize the traffic on the Proxyman app by project and device name. Therefore, it's easier to know where the request/response comes from.

## Troubleshooting
### 1. I could not see any request from Atlantis on Proxyman app?
For some reason, Bonjour service might not be able to find Proxyman app if you're in a company network. 

Please try to plugin your iOS Devices to your Macbook and try again. Bonjour services can discover by using a USB Cable.

## Credit
- FLEX and maintainer team: https://github.com/FLEXTool/FLEX
- @yagiz from Bagel project: https://github.com/yagiz/Bagel

## License
Atlantis is released under the Apache-2.0 License. See LICENSE for details.

