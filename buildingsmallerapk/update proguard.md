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
2. Another thing it does is it obfuscates names of types and methods and files, so that large names replace with the short strings like “c” and “z”. 
3. And the last thing it does is to eliminated dead code and this is the most important role of ProGuard.

## Dead Code Technique

Android apps have well known entry point at activities, services, receivers etc. If this classes are in app manifest the ProGuard marks them as live because this code can execute at runtime. ProGuard then propagates liveness across the program via references and whatever code remains is presumed dead and will be deleted from your app unless you specify ProGuard rules for that ().
