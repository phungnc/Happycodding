# Create environment of Cordova

## Overview

Cordova is open source that is used to create Application for iOS and Android by HTML5.
This Application is call Hybrid Application. When we run Application in Mobile, Cordova framework also work.
From Cordova3.0, we can manage Cordova Project by Node.js Command Line Tool.

## Introduction

1. Create Development environment
2. Create and Manage Project
3. Develop Application
4. Use Cordova plugin
5. Embed Cordova to an Application

### Create Development environment

#### Install Node.js

#### Install cordova Command Line Tool

- Windows

  ```
  npm install cordova -g
  ```

- Mac/Linux

  ```
  sudo npm install cordova -g
  ```

Confirm version

```
cordova -v
```

We need to add directory path in Android SDK to use internal Android SDK command.

```
/sdk/tools
```

and

```
/sdk/platform-tools
```

Go to
http://developer.android.com/sdk/index.html

Download Android SDK, install and remember path to sdk location.

```
$ echo "export PATH=$PATH:path/to/adt-bundle-mac-x86_64-20130729/sdk/tools/" ¥
  >> ~/.bash_profile
$ echo "export ¥
  PATH=$PATH:path/to/adt-bundle-mac-x86_64-20130729/sdk/platform-tools/" ¥
  >> ~/.bash_profile

$ source ~/.bash_profile
```

Confirm if Android Path is add successfully

```
$ android -h

  Usage:
  android [global options] action [action options]
  Global options:
  ...

$ adb version
Android Debug Bridge version 1.0.31
```

#### Create Project

After install cordova command, let create project.

```
cordova create hello com.example.hello HelloWorld -d
```
This command will create hello directory
-d option: display detail info when executing cordova command.


```
cd hello

cordova platform add ios
cordova platform add android
```

After run those command, this will create XCode Project for iOS.
We can use this command to add webOS or Windows Phone.

If you meet error when add android platform, follow below steps will solve it.

- Went into the SDK Manager (typing android into terminal)
- Find Android version that is need to add (for ex. Android 4.4.2 (API 19) )
- Check it
- Click button Install 8 packages

Run again command.

Use below command to check current platform of project

```
cordova platform ls
```

Use below command to remove a platform

```
cordova platform remove ios
```

#### Project structure


| hello/ |           | Description                                                                                    |
|--------|-----------|------------------------------------------------------------------------------------------------|
|        | .cordova  | cordova project configuration files                                                            |
|        | www       | HTML5 resource and App configuration files                                                     |
|        | platforms | Platforms                                                                                      |
|        | merges    | resource for platforms. Contain merged files that compile from www directory for each platform |
|        | plugins   | Cordova plugin                                                                                 |


#### Using Android emulator

To use Android Emulator, use cordova emulate

```
cordova emulate android -d
```


#### Using iOS emulator

Use ios-sim tool to simulate.

- Mac

```
brew install ios-sim
```

- Window

```

```

#### Run project on device

Set USB ON on Android Mobile, plug USB cable, then run cordova command

```
cordova run android
```

currently, Cordova is not supported for installation App by cordova command.
If you want to run it on devive, open project in Xcode

```
open platoforms/ios/HelloWorld.xcodeproj
```

#### Run on browser


```
cordova serve android
```

Ctrl + C to shutdown.


#### Manage cordova command

- Update cordova

```
npm update cordova -g
```

- Install specific version

```
npm install cordova@3.0.0 -g
```
