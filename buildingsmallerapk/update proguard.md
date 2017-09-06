ProGuard is enabled by default for release builds and it’s a whole program Java optimizer.

```gradle
android {
	buildtypes {
		release {
			minifyEnabled true
			}
		}
}
```
The ProGuard does three things. 
1. It optimizes your code in ways that don’t change the functionality but do changes representation to make it more compact.
2. Another thing it does is it obfuscates names of types and methods and files, so that large names replace with the short strings like `c` and `z`. 
3. And the last thing it does is to eliminated dead code and this is the most important role of ProGuard.

## Eliminating Dead Code Technique

Android apps have well known entry point at activities, services, receivers etc. If this classes are in app manifest the ProGuard marks them as live because this code can execute at runtime. ProGuard then propagates liveness across the program via references and whatever code remains is presumed dead and will be deleted from your app unless you specify ProGuard rules for that ([*learn more about proguard rules*](https://www.guardsquare.com/en/proguard/manual/usage)).

![dead code](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/apk_dimensions.jpeg)  

#### Results
Rebuilding and analysing my apk after this implementation yielded this result:
![dead code](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/apk_dimensions.jpeg) 

As you can see , most of the code is now completely gone and the app size is considerably smaller than it was before. You can use compare with button in APK analyzer and see the difference in “classes.dex” size and also you will see the code is obfuscated.
