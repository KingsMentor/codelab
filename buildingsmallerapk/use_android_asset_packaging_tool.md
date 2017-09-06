Google introduce a new update to AAPT, the AAPT2.<br/>
The AAPT is the part of the build system that process and package all your resources into the APK. The AAPT 2 is embedded by default in android studio 3.0 but it can be enable  in `canary version b` adding this line to gradle properties (`gradle.properties`).

```gradle
android.enable Aapt2 = true
```
### BEnefits

* Version Collapsing - involves figuring out the minimum version of your app and getting rid of all unnecessary resources that are not needed. It only includes the resource that your app would actually need.  
* Resource Deduplication - find duplicate resources, get rid of them and let the system default to default configurations.
* UTF-8 everywhere
* smarter cruncher - smartly reduces the size of your images by optimising them. If the  image size is bigger than the optimise image size, the optimisize image size is used. Your app image size is used if otherwise.

# Results
Here is the result so far on implementing this step.
