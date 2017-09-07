What has been done for code, can be done resources as well. Resource shrinking extend the concept of ProGuard dead code elimination to resources. Drawable and resource that are reference in your live code are kept or discarded if otherwise. To enable resource shrinking add this line to release build types:

```gradle
shrinkingResources true
```

# Results
Here is the result so far on implementing this step.<br/>
![using proguard result](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/enable_resource_shrinking.png) 


As you can see, I've been able to reduce the apk size by just 2 tricks so far, and there's more


