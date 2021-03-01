![image](https://github.com/JackTeam/InstagramThumbnail/raw/master/Screenshots/InstagramThumbnailGrid.gif)
![image](https://github.com/JackTeam/InstagramThumbnail/raw/master/Screenshots/InstagramThumbnailOnePicture.gif)

==================

InstagramThumbnail is a display thumbnail grid view, based on Instagram App.


Easy to drop into your project.      

You can add this feature to your own project, `InstagramThumbnail` is easy-to-use.        

## Requirements ##

InstagramThumbnail requires Xcode 5, targeting either iOS 6.0 and above, ARC-enabled.      

## Profile

[CocosPods](http://cocosPods.org) is the recommended methods of installation InstagramThumbnail, just add the following line to `Profile`:

```
pod 'InstagramThumbnail', '~> 0.1.0'
```

## How to use ##
```objc
Use this library setup grid thumbnail to show:
InstagramCollectionViewController *instagramCollectionViewController = [InstagramPictureCollectionViewController sharedInstagramPictureCollectionViewController];
    instagramCollectionViewController.showThumbnail = YES;
    self.window.rootViewController = [[UINavigationController alloc] initWithRootViewController:instagramCollectionViewController];

Use this library setup one pictre to show:
InstagramCollectionViewController *instagramCollectionViewController = [InstagramPictureCollectionViewController sharedInstagramPictureCollectionViewController];
    instagramCollectionViewController.showThumbnail = NO;
    self.window.rootViewController = [[UINavigationController alloc] initWithRootViewController:instagramCollectionViewController];

```
## Lincense ##

`InstagramThumbnail` is available under the MIT license. See the LICENSE file for more info.


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)