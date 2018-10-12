# cordova-plugin-inappbrowser-wkwebview

- This is a fork of [cordova-plugin-inappbrowser](https://github.com/apache/cordova-plugin-inappbrowser) 
- It uses the the newer [WKWebview](https://developer.apple.com/documentation/webkit/wkwebview) to power the InAppBrowser, in contrast to `cordova-plugin-inappbrowser` which still currently uses the legacy [UIWebView](https://developer.apple.com/documentation/uikit/uiwebview).
- Only the iOS platform has been changed from the original `cordova-plugin-inappbrowser`.
- The plugin supports iOS 9 and above
    - While WKWebView was introduced in iOS 8, it contained critical bugs making it effectively unusable for Cordova-based apps
    
Some advantages of using WKWebView over UIWebView include:

- Performance: graphic-intensive operations such as WebGL run much faster and more efficiently in WKWebView.
- Stability: WKWebView has many improvements which leads to up to 70% less crashes.
- Shared cookies: setting a cookie in an IAB window makes it available in the main Cordova Webview and vice-versa. This is especially useful for cookies that store authentication credentials since they will be preserved between IAB sessions.
    
## Installation

    cordova plugin add cordova-plugin-inappbrowser-wkwebview
    cordova plugin add cordova-plugin-wkwebview-engine

- This plugin depends on [cordova-plugin-wkwebview-engine](https://github.com/apache/cordova-plugin-wkwebview-engine) which adds WKWebView support to Cordova.
- You need to add this (or a variant) manually to your project
- This means the main Cordova app Webview will also use WKWebView on iOS 9+.

## Example app

[cordova-plugin-inappbrowser-wkwebview-test](https://github.com/dpa99c/cordova-plugin-inappbrowser-wkwebview-test) contains a Cordova project which builds an iOS test app to validate/illustrate usage of this plugin.

## Related plugin

[cordova-plugin-inappbrowser-popup-bridge](https://github.com/dpa99c/cordova-plugin-inappbrowser-popup-bridge) is an extension of this plugin which adds support for Braintree's PopupBridge libraries for [Android](https://github.com/braintree/popup-bridge-android) and [iOS](https://github.com/braintree/popup-bridge-ios) to support PayPal payments within the context of the InappBrowser element of a Cordova-based app.

## Plugin usage and API

The plugin API is identical to [cordova-plugin-inappbrowser](https://github.com/apache/cordova-plugin-inappbrowser).

## Additional functions for this fork:
- Additional listeners for url changes (for SPA's). Usage:
```javascript
InAppBrowser.addEventListener('urlchanged', yourCallback);
```

- Changing status bar colors. For Android, IAB covers the status bar, so an adjustment has been made for the IAB size. For iOS, the status bar did not seem to work, so additional handlers were added. Usage:
```javascript
InAppBrowser.changeToolBar('#000000', 'light', () => { });
```
- first argument: hex color
- second argument: 'light' or 'dark' (for icon colors against the status bar backdrop);
