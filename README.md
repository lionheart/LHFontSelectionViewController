LHFontSelectionViewController
=============================

This view controller gives you a quick and easy way to let users of your app browse through the list of available fonts on their iOS device.

![image](https://f.cloud.github.com/assets/38447/1774203/888a8b06-67f5-11e3-9187-c1b1c9e415c0.png)

Installation
------------

Cocoapods is the recommended installation method. Just add this line to your Podfile.

    pod 'LHFontSelectionViewController', :git => 'https://github.com/lionheart/LHFontSelectionViewController.git'

Usage
-----

Integration LHFontSelectionViewController into your project is pretty straightforward. You just need to instantiate the controller, assign a delegate, and then define the required methods in your delegate.

Here's a quick example:

```objc
LHFontSelectionViewController *fontSelectionViewController = [[LHFontSelectionViewController alloc] init];
fontSelectionViewController.delegate = self;
[self.navigationController pushViewController:fontSelectionViewController];
```

Your delegate must conform to LHFontSelecting, which defines these methods:

```objc
fontNameForFontSelectionViewController:
setFontName:forFontSelectionViewController:
fontSizeForFontSelectionViewController:
```

The above implementation lets you be flexible in how your implement LHFontSelectionViewController. Here's an example of how I'm using them in a production app:

```objc
#pragma mark - LHFontSelecting

- (NSString *)fontNameForFontSelectionViewController:(LHFontSelectionViewController *)viewController {
    return [[NSUserDefaults standardUserDefaults] stringForKey:SettingsFontNameKey];
}

- (void)setFontName:(NSString *)fontName forFontSelectionViewController:(LHFontSelectionViewController *)viewController {
    [[NSUserDefaults standardUserDefaults] setObject:fontName forKey:SettingsFontNameKey];
}

- (CGFloat)fontSizeForFontSelectionViewController:(LHFontSelectionViewController *)viewController {
    return [Theme fontSize] + 4;
}
```
