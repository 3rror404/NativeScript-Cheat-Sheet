# NativeScript-Cheat-Sheet
Often used. Rarely remembered.

---

### Contents

* [CLI](#cli)
 * [Update `tns-core-modules` and `tns-core-modules-widgets`](#update-tns-core-modules-and-tns-core-modules-widgets)

* [Visual](#visual)
 * [iOS Blurred background modal](#ios-blurred-background-modal)
 * [iOS Drop Shadow](#ios-drop-shadow)

---

# CLI

Update `tns-core-modules` and `tns-core-modules-widgets`
---

```
$ tns plugin remove tns-core-modules
$ tns platform remove android
$ tns platform remove ios
$ tns plugin add tns-core-modules
$ tns platform add android
$ tns platform add ios
```

Add signing identity to xcode project.


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

