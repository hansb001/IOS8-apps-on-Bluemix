IOS8-apps-on-Bluemix https://www.ng.bluemix.net/docs/#starters/mobilefirst/gettingstarted/index.html#gettingstarted
===Creating an iOS 8 app in Bluemix

Create a mobile application in the Bluemix dashboard.

In the Bluemix dashboard, click Create an app > Mobile > iOS 8.
When you create the app in the Bluemix dashboard, a unique App ID is assigned to your application. A Node.js runtime is created so that you can provide server-side functions, such as resource URIs and static files. The Cloudant NoSQL DB, Push for iOS8, and Advanced Mobile Access services are added to the app.
Installing the IBM MobileFirst Platform for iOS Client SDK using CocoaPods

You can set up the IBM MobileFirst Platform for iOS Client SDK using the CocoaPods dependency management tool. An alternative is to install the SDK manually.

Installing CocoaPods

Install CocoaPods by using the following command in your Mac terminal:
$ sudo gem install cocoapods
Create a file that is called podfile in your Xcode project folder. In that file, list the SDK dependencies you need. You can copy the set of commands that appears after the next table as is and remove the dependencies that you do not need.
For	Include
Facebook authentication	IMFFacebookAuthentication
Google authentication	IMFGoogleAuthentication
Custom authentication	IMFCore
NSURLRequest	IMFURLProtocol
Analytics	IMFCore
Push	IMFPush
Data	CloudantToolkit
source 'https://github.com/CocoaPods/Specs.git'
# Copy the following list as is and remove the dependencies you do not need
pod 'IMFCore'
pod 'IMFGoogleAuthentication'
pod 'IMFFacebookAuthentication'
pod 'IMFURLProtocol'
pod 'IMFPush'
pod 'CloudantToolkit'
After you have modified your podfile with the wanted dependencies, enter your project folder from your terminal and install the dependencies using the following command:
pod install
That command installs your dependencies and creates a new Xcode workspace.
Note: Ensure that you always open the new Xcode workspace, instead of the original Xcode project file:
$ open App.xcworkspace
The workspace contains your original project and Pods project that contains your dependencies. If you would like to modify an IBM MobileFirst Platform for iOS source folder, you can find it in your Pods project, under Pods/yourImportedSourceFolder, for example: Pods/IMFGoogleAuthentication.
Using imported frameworks and source folders

Reference the SDK in your code.
In Objective-C:
Write #import directives for the relevant headers, for example:
#import <IMFPush/IMFPush.h>
#import "IMFURLProtocol.h"
.
Note: Updating your Pods project using the CocoaPods commands pod install or pod update might override the IBM MobileFirst Platform for iOS source folders. If you wish to retain your customized versions of the original files, ensure that you have backed them up before issuing one of these commands.
For more information

Getting Started with CocoaPods at: CocoaPods.org
Apple documentation at: Swift and Objective-C in the Same Project
Manually installing the IBM MobileFirst Platform for iOS Client SDK

You can set up Xcode to work with the IBM MobileFirst Platform for iOS Client SDK .zip file you have downloaded manually. An alternative is to install the SDK using CocoaPods.

Download the IBM MobileFirst Platform for iOS SDK and select an Xcode project and app

Download the SDK .zip file and extract the contents to a convenient location.
In the Xcode project navigator, select or create the project with which to associate the SDK.
In Targets lists, select your application target.
Add libraries

Click the Build Phases tab at the top of the project settings pane.
Click Link Binary With Libraries to add the necessary IBM MobileFirst modules to the project:
Click + located under the list. The Choose frameworks and libraries to add dialog appears.
Click Add Other. A file chooser appears.
Navigate to the IBM MobileFirst Platform for iOS SDK installation folder that contains the files you extracted and select the following frameworks:
IMFCore.framework (mandatory)
IMFPush.framework (if you are using Push for iOS8)
CloudantToolkit.framework (if you are using Cloudant NoSQL DB)
Add the following Cocoa Touch frameworks:
Foundation.framework
SystemConfiguration.framework
Security.framework
MediaPlayer.framework
CoreText.framework
CoreGraphics.framework
CoreMotion.framework
CoreLocation.framework
AssetsLibrary.framework
AddressBook.framework
If you want to use the default IBM MobileFirst Platform for iOS implementation of NSURLProtocol, copy to your project the sources in the IMF-iOSClientSDK/Sources/Authenticators/IMFURLProtocol folder.
Add build settings

Click the Build Settings tab at the top of the project settings pane.
Add the -ObjC flag to the Linking | Other Linker Flags field.
In Build Settings, scroll down to the Apple LLVM 6.0 – Language – Modules section. Set the Allow Non-modular Includes In Framework Modules option to Yes.
Copy authentication-related sources to your project

Do one of the following:
For Facebook authentication:
Copy sources that are related to IMFFacebookAuthentication to the IMF-iOSClientSDK/Sources/Authenticators/IMFFacebookAuthentication folder.

More information: Using Facebook as an identity provider
For Google authentication:
Copy sources that are related to IMFGoogleAuthentication to the IMF-iOSClientSDK/Sources/Authenticators/IMFGoogleAuthentication folder.

More information: Using Google as an identity provider
(Optional) Downloading the Bluelist sample app

If you don't already have an app that you're developing, you can download a sample. The Bluelist sample app is available in Swift and Objective C. This sample demonstrates how to use the core pieces of the SDK, including data CRUD operations, Push notifications, security, and monitoring.

Download sample: Bluelist sample
Initializing the SDK

Update your client application to connect with the mobile app you created in the Bluemix dashboard.

Initialize the SDK. Get the route and appID information from the IBM Advanced Mobile Access for Bluemix service instance in your app. Click app_name > Advanced Mobile Access > Client registration. The values to use are listed as the Route and UID.
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:applicationRoute backendGUID:appId];
Writing a Swift app with the SDK

You can set up a Swift app project in the same manner you set up an Objective-C project.

Sample app

When the project is set up, you can use SDK classes in the same way as you would used CocoaTouch classes from Swift.
Importing sample code into Swift projects

You can import the sample source code that is supplied with the IBM MobileFirst Platform for iOS SDK into Swift applications. Because the SDK source is written in Objective-C, the result is a “ mixed mode ” application, containing Swift and Objective-C statements.
Select File | Add Files to <project_name> and add appropriate sources to the project. You can add IMFURLProtocol, IMFGoogleAuthentication or IMFFacebookAuthentication handlers.
Continue with the steps for Swift.
For more information and troubleshooting, see Swift and Objective-C in the Same Project.
Next steps: Adding security, monitoring, data and push notifications to your app

After you have set up your development environment, you can start developing your application.

Add functionality from the IBM MobileFirst Platform for iOS SDK to your iOS app.
To add security and monitoring, see IBM Advanced Mobile Access for Bluemix
To store data, see Cloudant NoSQL DB
To implement push notifications, see IBM Push for iOS8 for Bluemix=================
