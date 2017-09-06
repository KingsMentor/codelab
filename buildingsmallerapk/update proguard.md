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
