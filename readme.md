## OpenCV-Repackaged

### What exactly is this?

This is the OpenCV Java API, repackaged into an AAR that you can add as a Gradle dependency to your Android Studio project. This is exactly the same thing that is in the `/sdk/java` folder of the OpenCV Android bundle.

### Why in the world would I want to use this?

To avoid the pain of having to download the OpenCV Android bundle, extract the Java library, and import it as a module in Android Studio. This bloats your git repository and makes it a pain to upgrade to a newer OpenCV version.
**However, that's not even the biggest benefit of using this library!** To decrease the final APK size (and thus decreasing deployment time to your robot each time you make a code change), this library loads the C++ library required by OpenCV (more than 10MB!) dynamically from the internal storage instead of shipping it inside the APK.

### So how do I use this?

1. Open your FTC SDK Android Studio project
2. Open the `build.common.gradle` file:

    ![img-her](doc/images/build-common-gradle.png)

3. Add `jcenter()` to the `repositories` block at the bottom:

    ![img-her](doc/images/jcenter.png)

4. Open the `build.gradle` file for the TeamCode module:

    ![img-her](doc/images/teamcode-gradle.png)

5. At the bottom, add this:

        dependencies {
            implementation 'org.openftc:opencv-repackaged:4.1.0-A'
         }

6. Copy `libOpenCvNative.so` from the `/doc` folder of this repo into the `FIRST` folder on the internal storage of the Robot Controller

7. You can now use OpenCV just as you would as if you had manually imported the module, with one minor difference being you do **not** need to call any methods such as `OpenCVLoader.initDebug()` because the native library is automatically loaded in the background when the SDK boots.

## Changelog:

#### v4.1.0-A

 - Initial release, based on OpenCV Android SDK v4.1.0
