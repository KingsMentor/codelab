As saw in the resource folder, taking a look at the APK analyzer, you will notice that there are different drawables for different screen density. The android ecosystem is diverse and there is support for different displays and different CPUs.
There are basically 2 kinds of apk that can be an output from a build.<br>
1. **Universal Apk** - tailored to work on all supported devices (based on your gradle configurations). This result to a larger apk than what is particularly needed on each devices. Every specific device that runs your app will only use files for its particular configuration.
2. **Multiple Apk** - your build is splited into different dimension and uploaded to Google play, each one tailored to a particular device type. This helps reduce the size of the apk on different devices. 

Here's how you can achieve that.

```gradle

android { 
	splits {
		density {
			enable true
			}
		}
	}
  
```

This step can be very ellaborate, as you can split your apk base on multiple configurations. 

Here are some of the ways:

### ABI split

This is especially useful if your project includes libraries written in native code (.so files) which support different CPU architectures. You can split your APK per architecture so that a user running an arm ABI doesn’t receive the code for x86, and so on. To do this, add the following to your app level build.gradle file:

```gradle
android {
...
    splits {
        abi {
            enable true
            reset()
            include 'x86', 'armeabi-v7a', 'mips'
            universalApk false
        }
    }
...

}
```

### Density level split

Using this you can produce multiple APKs split by the density of the device so that a user with a xhdpi device doesn’t carry assets meant for xxxhdpi. To do this, add the following to your app level build.gradle file:

```gradle
android {
    splits {
        abi {
            enable true
            reset()
            universalApk false
            include 'mdpi', 'hdpi', 'xhdpi', 'xxhdpi', 'xxxhdpi'
        }
    }
}
```

For a comprehensive list of more split option, see [here](https://developer.android.com/google/play/publishing/multiple-apks.html#HowItWorks) 

# Results
Here is the result so far on implementing this step.<br/>
![multiple apks](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/multiple_apks.png) 

As you can see, the apks size has been drastically being reduced. Google play hanldes serving different apk based on device configuration. Let's take a look at `app-X86-debug.apk` (which happens to be the largest file in there). <br/>
![analysing multiple apk](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/multple_apk_result.png) 

Great output right ? There's more !

