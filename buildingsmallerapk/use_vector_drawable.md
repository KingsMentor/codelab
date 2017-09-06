As seen in the previous step, creating multiple apk based on screen density, helped reduced apk size for each device type. This however, comes with some cost on your build process and quality assurance process. Continuing with it means you are ready to get into all of that.<br/>
Another way to reduce the amount of size you carry with your assets is to use vector drawables instead of PNGs.<br/>
Vector drawable allows you to use one asset for all densities. <br/><br/>

<aside class="special" <p> One thing to keep in mind with vectors is that they can increase your RAM and CPU load, especially when you first start up the application so it is better to do a bit of performance test.</p></aside>

Use vector drawables have some benefits in comparison to multi APKs because it simplify your Quality Assurance process and upload one APK.
you can download vector drawable for popular icons at [materialdesignicons](https://materialdesignicons.com/) and if you are new to this, [here](https://medium.com/@ali.muzaffar/understanding-vectordrawable-pathdata-commands-in-android-d56a6054610e) is a good place to get started.

To enable use of vector drawable, add this to gradle.

```gradle
android {
	defaultConfigs {
			vectorDrawables.useSupportLibrary true
			}
	}
```

# Results
Here is the result so far on implementing this step.
