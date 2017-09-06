Fonts are a source of bloat for apps, and they are heavy files. But you need them because you need it for UX. Several apps are bundling the same fonts, and you’re duplicating them in your device. You typically bundled fonts in your app and that causes your APK size to increase as some of the fonts are not really optmize for mobile.

Downloadable fonts use a concept of a font provider. Font provider is a separate app that its own mission to fetch fonts, cache them, and serve them when needed.
All apps should contact to font provider via the font’s contract APIs. This means we have one copy of the font that all apps using the same time.

### Font Provider Illustration


Benefits of using downloadable fonts:

1. This approach helps save memory (only the font needed is loader) , and font memory space is shared across apps in same device.
2. Saving apk size. You don't need to bundle fonts along with your build.
3. Saving network call (if you needed to pull the font from the network). The font provider handles both pulling and caching of neccessary fonts.
4. Entire catalog of Google fonts (over 800 of them) is available to your app.

You can find more details about this [here](https://developer.android.com/guide/topics/ui/look-and-feel/downloadable-fonts.html).

# Results
Here is the result so far on implementing this step.
