## Kotlin example for the SwiftAndroid toolchain.

Requires a build of the latest Android toolchain downloadable [here](http://johnholdsworth.com/android_toolchain.tgz). Once you've extracted the toolchain, run `swift-install/setup.sh` to get started. Once you've extracted this example you may need to edit local.properties to point to your Android SDK and then you should be able to run `./gradlew installDebug` or build the project in Android Studio. Make sure the that the `ANDROID_HOME` environment variable is set to the path to the SDK.
The phone must be api 21 aka Android v5+ aka Lollipop or better (I used an LG K4.) 
To create a new application, decide on a pair of interfaces to connect to and from your Swift
code and place them in a [Java Source](https://github.com/SwiftJava/swift-android-samples/blob/master/swifthello/src/main/java/com/jh/SwiftHello.java).
Use the command `./genswift.sh` in the [SwiftJava Project](https://github.com/SwiftJava/SwiftJava)
to generate Swift (& Java) sources to include in your application or adapt the
[genhello.sh](https://github.com/SwiftJava/SwiftJava/blob/master/genhello.sh) script.
If you only use interfaces/protocols, your app's only
[Package.swift](https://github.com/SwiftJava/swift-android-samples/blob/master/swifthello/src/main/swift/Package.swift)
dependency should be the core JNI interfacing code [java_swift](https://github.com/SwiftJava/java_swift).

This example is coded to work with version 4 of the toolchain which has some additional requirements
to work around requirements of the Swift port of Foundation. The cache directory used by web operations
needs to be setup in the environment variable "TMPDIR". This would usually be the value of
Context.getCacheDir().getPath() from the java side. In addition, to be able to use SSL you
need to add a [CARoot info file](http://curl.haxx.se/docs/caextract.html) to the application's
raw resources and copy it to this cache directory to be picked up by Foundation as follows:

    URLSession.sslCertificateAuthorityFile = URL(fileURLWithPath: cacheDir! + "/cacert.pem")

If you don't want peer validation you have the following option (not recommended at all)

    URLSession.verifyPeerSSLCertificate = false

##

Simple demo of Swift code accessed over JNI.

To build, setup the Gradle plugin, then run `./gradlew installDebug`

This demo is licensed under the Creative Commons CC0 license:
do whatever you want.
