# ConnectedSDK for iOS(Objective-C)

## Requirements

1. XCode 10 - (XCode 11 support is under development)

## Installation
### Installation with CocoaPods
[CocoaPods](https://cocoapods.org/) is a dependency manager for Swift and Objective-C Cocoa projects, which automates and simplifies the process of using 3rd-party libraries like the ConnectedAdSDK in your projects. You can install it with the following command:
```
$ sudo gem install cocoapods
```

**Podfile**  To integrate ConnectedSDK into your Xcode project using CocoaPods, specify it in your Podfile:
```
pod 'ConnectedSDKiOS_ObjC', :git => 'https://github.com/connsdkimpl/Connected_ObjC.git'
```

Then, run the following command:
```
$ pod install
```
Note: Make sure  [Connected_ObjC](https://github.com/connsdkimpl/Connected_ObjC) is public.
## Integration
### 1. Configure Ad Units in Your App
In your app’s `AppDelegate.m` file, in  `application didFinishLaunchingWithOptions:` method,  use the following code:
```
[ConnectedAd getConnectedAdDetails:@"YOUR_APP_ID"];
```
in `Info.plist` file, add `<key>GADApplicationIdentifier</key><string>YOUR_GADAPPLICATIONIDENTIFIER</string>` to include the `GADApplicationIdentifier` from AdMob.

### 2. Loading Banner Ads
#### Step 1. Edit Your View Controller’s Header File

In your view controller’s header file, import the ```ConnectedAdBanner.h``` header file and declare an ```ConnectedAdBanner *connectedAdBanner``` property.

```
// MyViewController.h

#import "ConnectedAdBanner.h"

@interface MyViewController : UIViewController
{
  @property (nonatomic) ConnectedAdBanner *connectedAdBanner;
}

@end

```

#### Step 2. Edit Your View Controller’s Implementation File

Initialise the following properties to your ConnectedAdBanner.

```
self.connectedAdBanner = [[ConnectedAdBanner alloc]initWithFrame:BANNER_FRAME];
self.connectedAdBanner.adMobConnectedId = @"ADMOB_BANNER_CONNECTED_ID";
self.connectedAdBanner.moPubConnectedId = @"MOPUB_BANNER_CONNECTED_ID";
self.connectedAdBanner.rootViewController = self;
self.connectedAdBanner.delegate = self;
self.connectedAdBanner.bannerSize = small(or medium if u need a larger one);
[self.view addSubview:connectedAdBanner];
```
Whenever you need to present your banner, call ```loadAds``` of your **ConnectedAdBanner** to load and display the ad.
```
[self.connectedAdBanner loadAds];
```
Note: If you don't have any of the connected Ids, then there is no need to set values to corresponding properties.

### 3. Loading Interstitial Ads
#### Step 1. Edit Your View Controller’s Header File

In your view controller’s header file, import the ```ConnectedAdInterstitial.h``` header file and declare an ```ConnectedAdInterstitial *connectedAdInterstitial``` property.

```
// MyViewController.h

#import "ConnectedAdInterstitial.h"

@interface MyViewController : UIViewController
{
    @property (nonatomic) ConnectedAdInterstitial *connectedAdInterstitial;
}

@end

```

#### Step 2. Edit Your View Controller’s Implementation File
Initialise the **ConnectedAdInterstitial** object created.
```
self.connectedAdInterstitial = [[ConnectedAdInterstitial alloc] init:@"ADMOB_INTERSTITIAL_CONNECTED_ID" :@"MOPUB_INTERSTITIAL_CONNECTED_ID" ];
self.connectedAdInterstitial.delegate = self;
```
Whenever you need to show your interstitial ad, call ```loadFrom``` of your **ConnectedAdInterstitial** to load and display the same.
```
[self.connectedAdInterstitial loadFrom:self];
```
Note: If you don't have any of the ConnectedIds, then please set an empty string ```@""``` for the corresponding item.

For example, if your app does not have MoPub integrated, then create a **ConnectedAdInterstitial** instance like this:

```
self.connectedAdInterstitial = [[ConnectedAdInterstitial alloc] init:@"ADMOB_INTERSTITIAL_CONNECTED_ID" :@"" ];
```
### 4. Loading Rewarded Video Ads
#### Step 1. Edit Your View Controller’s Header File

In your view controller’s header file, import the ```ConnectedAdRewarded.h``` header file and declare an ```ConnectedAdRewarded *connectedAdRewarded``` property.

```
// MyViewController.h

#import "ConnectedAdRewarded.h"

@interface MyViewController : UIViewController
{
    @property (nonatomic) ConnectedAdRewarded *connectedAdRewarded;
}

@end

```

#### Step 2. Edit Your View Controller’s Implementation File
Initialise the **ConnectedAdRewarded** object created.
```
self.connectedAdRewarded = [[ConnectedAdRewarded alloc] init:@"ADMOB_REWARDED_CONNECTED_ID" :@"MOPUB_REWARDED_CONNECTED_ID" ];
self.connectedAdRewarded.delegate = self;
```
Whenever you need to show your interstitial ad, call ```loadFrom``` of your **ConnectedAdRewarded** to load and display the same.
```
[self.connectedAdRewarded loadFrom:self];
```
Note: If you don't have any of the ConnectedIds, then please set an empty string ```@""``` for the corresponding item.

For example, if your app does not have MoPub integrated, then create a **ConnectedAdRewarded** instance like this:

```
self.connectedAdRewarded = [[ConnectedAdRewarded alloc] init:@"ADMOB_REWARDED_CONNECTED_ID" :@"" ];
```
### 5. Implementing Delegates
#### Step 1. Edit Your View Controller’s Header File
Conform your ViewController to ```ConnectedAdDelegate``` protocol.
```
// MyViewController.h
@interface MyViewController : UIViewController <ConnectedAdDelegate>

@end
```
#### Step 2. Edit Your View Controller’s Implementation File

Implement all the methods.
```
- (void)connectedAdDidFailToReceiveAd:(AdType)adType withError:(NSError * _Nullable)error {
  NSLog(@"delegate ad error from:%ld, Error:%@", (long)adType, error.localizedDescription);
}

- (void)connectedAdReceivesAd:(AdType)adType {
  NSLog(@"delegate ad error from:%ld", (long)adType);
}
```
## License
MIT License

Copyright (c) 2019 connsdkimpl

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
