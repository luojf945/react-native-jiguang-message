# Quick Start
use`npm`install
```shell
npm install --save react-native-jiguang-message@latest
```
## RN Link Command
Please input appKey and masterSecret while running`react native link`.
```shell
 react-native link react-native-jiguang-message
```
## Manual Link

### iOS

* Open your app's Xcode project

* Find the `RCTJMessage.xcodeproj` file within the `node_modules/react-native-jmesjiguang-messagesage/ios` directory  and drag it into the `Libraries` node in Xcode

* Select the project node in Xcode and select the "Build Phases" tab of your project configuration.

* Drag `libRCTJMessage.a` from `Libraries/RCTJMessage.xcodeproj/Products` into the "Link Binary With Libraries" section of your project's "Build Phases" configuration.

* Click the plus sign underneath the "Link Binary With Libraries" list and add the `libz.tbd,libsqlite3.tbd,libresolv.tbd,UIKit.framework,Foundation.framework,
SystemConfiguration.framework,CoreFoundation.framework,CFNetwork.framework,
Security.framework,CoreTelephony.framework` library .

* Click the plus sign underneath the "Link Binary With Libraries" list and add the JMessage.framework which locate in `../node_modules/react-native-jiguang-message/ios/RCTJMessage` and the jcore-ios-1.1.0.a which locate in `../node_modules/react-native-jiguang-message/ios/RCTJMessage/JMessage.framework`. Then Under the "Build Settings" tab of your project configuration, find the "Framework Search Paths" section and edit the value. Add a new value, `$(SRCROOT)/../node_modules/react-native-jiguang-message/ios/RCTJMessage/**`.

* add following code to your AppDelegate.m 
```objectiv-c
...
#import <JMessageModule/RCTJMessageModule.h>
```
* add following code to didFinishLaunchingWithOptions method
```objectiv-c
[JMessage registerForRemoteNotificationTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil];
	#ifdef DEBUG
	[RCTJMessageModule setupJMessage:launchOptions apsForProduction:false category:nil];
	#else
	[RCTJMessageModule setupJMessage:launchOptions apsForProduction:true category:nil];
	#endif
```
* add JiguangAppKey、JiguangMasterSecret and JiguangAppChannel into Info.plist

### Android

* In your `android/settings.gradle` file, make the following additions:

    ```gradle
    include ':react-native-jiguang-message'
project(':react-native-jiguang-message').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-jiguang-message/android')
    ```

* In your `android/app/build.gradle` file, add the `:react-native-jiguang-message` project as a compile-time dependency:

    ```gradle
    ...
    dependencies {
        ...
        compile project(':react-native-jiguang-message')
    }
    ```
* add AppKey、AppChannel and MasterSecret to `android/build.gradle` which locate in react-native-jiguang-message node_modules folder

    ```gradle
    ...
  manifestPlaceholders = [
            JIGUANG_APPKEY: ${JIGUANG_APPKEY},
            JGUANG_APPCHANNEL: "developer-default",
            JIGUANG_MASTER_SECRET: ${JIGUANG_MASTER_SECRET}
        ]
    ```
* Update the `MainApplication.java` file to use react-native-jiguang-message via the following changes:

```java
...
import com.xsdlr.rnjmessage.JMessagePackage;

public class MainApplication extends Application implements ReactApplication {

    private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
        ...

        @Override
        protected List<ReactPackage> getPackages() {
            return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                new JMessagePackage(BuildConfig.DEBUG)
            );
        }
    };
}
```

