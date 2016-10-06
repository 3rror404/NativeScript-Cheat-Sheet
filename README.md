# NativeScript-Cheat-Sheet
Often used. Rarely remembered.

---

### Contents

* [CLI](#cli)
 * [Update `tns-core-modules` and `tns-core-modules-widgets`](#update-tns-core-modules-and-tns-core-modules-widgets)

* [Visual](#visual)
 * [iOS Blurred background modal](#ios-blurred-background-modal)
 * [iOS Drop Shadow](#ios-drop-shadow)
 * [iOS TabView icons are grey when deselected](#ios-tabview-icons-are-grey-when-deselected)

---

# CLI

Update `tns-core-modules` and `tns-core-modules-widgets`
---

```
$ tns plugin remove tns-core-modules
$ tns platform remove android
$ tns platform remove ios
```
Current release version
```
$ tns plugin add tns-core-modules
```
@next version
```
$ tns plugin add tns-core-modules@next
```
Specific version
```
$ tns plugin add tns-core-modules@2.4.0-2016-10-05-4321
```
```
$ tns platform add android
$ tns platform add ios
```

**Don't forget!** - Add signing identity to xcode project.

All in one - `tns plugin remove tns-core-modules && tns platform remove android && tns platform remove ios && tns plugin add tns-core-modules@next && tns platform add android && tns platform add ios`

# Visual

iOS Blurred background modal
---

```
var Platform = require('platform');

if (Platform.isIOS) {
    page.ios.providesPresentationContextTransitionStyle = true;
    page.ios.definesPresentationContext = true;
    page.ios.modalPresentationStyle = UIModalPresentationStyle.UIModalPresentationOverFullScreen;
    page.ios.view.backgroundColor = UIColor.clearColor;

    // SET BLURRED BACKGROUND
    var pageBounds = page.ios.view.bounds;
    var navEffectView = UIVisualEffectView.alloc().initWithEffect(UIBlurEffect.effectWithStyle(UIBlurEffectStyleLight));
    navEffectView.frame = {
        origin: { x: 0, y: 0 },
        size: { width: pageBounds.size.width, height: pageBounds.size.height }
    };
    navEffectView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
    page.ios.view.addSubview(navEffectView);
    page.ios.view.sendSubviewToBack(navEffectView);
}
```

iOS Drop Shadow
-----

```
var Platform = require('platform');
var colorModule = require("color");
  
if (Platform.isIOS) {
  var myElement = page.getViewById('myElement');
  myElement.ios.layer.masksToBounds = false;
  myElement.ios.layer.shadowOpacity = 1.0;
  myElement.ios.layer.shadowRadius = 1.0;
  myElement.ios.layer.shadowColor = new colorModule.Color('rgba(0,0,0,0.2)').ios.CGColor;
  myElement.ios.layer.shadowOffset = CGSizeMake(0, 2.0);
}
```

iOS TabView icons are grey when deselected
---

See this issue: https://github.com/NativeScript/nativescript-angular/issues/395#issuecomment-239472063

* navigate to `node_modules/tns-core-modules/ui/tab-view`
* open `tab-view.ios.js`
* at line 285 (as of tns-core-modules v2.4.0-2016-09-21-4189) find the following line
```
var originalRenderedImage = is.ios.imageWithRenderingMode(0);
```
change to
```
var originalRenderedImage = is.ios.imageWithRenderingMode(1);
```
