---
id: build-android
title: Build a Feathers UI project as an Android app
sidebar_label: Android
---

[Feathers UI](/) may be used to build mobile applications targeting Google's Android operating system.

## Prerequisites

In addition to the dependencies specified in the [Feathers UI installation instructions](./installation.md), building an Android application with Feathers UI has some additional requirements.

- [Install the Java OpenJDK](https://adoptopenjdk.net/) (version 8 or newer)

- [Download Android Studio](https://developer.android.com/studio)

  - Launch Android Studio at least once to go through its setup wizard that downloads the Android SDK components.

- [Download Android NDK **r15c**](https://developer.android.com/ndk/downloads/older_releases) (do not download a newer NDK version)

  - Extract the archive somewhere on your file system, and take note of the absolute path because it will be used in a later step.

### Configure OpenFL for Android

To set the locations of various tools required to build Android apps, you need to run the following command:

```hx
openfl setup android
```

It will request the paths to several of the required tools that were installed in previous steps.

#### Android SDK

Pass in the absolute path of the Android SDK.

> Run Android Studio at least one time to go through its setup wizard that downloads the Android SDK components.

Typically, when the Android SDK is installed by Android Studio, it is located at a standard location on each platform:

- Windows: _C:\Users\\**username**\AppData\Local\Android\Sdk_
- macOS: _~/Library/Android/sdk_
- Linux: _~/Android/Sdk_

#### Android NDK

Pass in the absolute path where you extracted the Android NDK.

#### Java JDK

The Java JDK may be installed in a variety of locations, depending on which operating system you are using:

- Windows: Typically, Java is installed to _C:\Program Files\AdoptOpenJDK_ or _C:\Program Files\Java_
- macOS: Run the **/usr/libexec/java_home** command in the Terminal app to find the JDK location.
- Linux: Run the **whereis java** command in a terminal to find the JDK location. `JAVA_HOME` should be set to parent of the _bin_ folder that contains the **java** executable.

## Build

To build for the `android` target, run the following command.

```sh
openfl build android
```

Use the `-debug` flag to create a build to include extra debugging information, including full stack traces when there's an exception or crash.

```sh
openfl build android -debug
```

The build's output will be written to the _bin/android/bin_ folder. The _.apk_ file may be found in _bin/android/bin/app/build/outputs/apk/debug_ (including release builds).

> Your [_project.xml_ file](https://lime.software/docs/project-files/xml-format/) may optionally specify an output folder different from _bin_.
>
> ```xml
> <app path="Export"/>
> ```
>
> In the example above, the output would be generated in _Export/android/bin_ instead.

## Troubleshooting

### Error: arm-linux-androideabi-g++: command not found

There is more than one possible reason for seeing this error:

1. You may have downloaded the wrong version of the Android NDK. You must use **r15c** specifically. Newer versions will not work.

1. You may have used the wrong path to the Android NDK on your file system. Check that the root folder of the SDK contains multiple sub-folders and files, including a README file.

> ### Did you get some other error message that you don't understand?
>
> Configuring OpenFL to build for native targets, like iOS or Android, can be a little tricky! Head over to either the [Feathers UI community forum](https://community.feathersui.com/) or the [Feathers UI Discord](https://discord.feathersui.com/). Explain which command you tried to run, be sure to mention that you are targeting **android**, and post the error message (and any additional relevant output). Ideally, we can help you figure out a solution, and then we'll also add it to this troubleshooting section, so that everyone can benefit.
