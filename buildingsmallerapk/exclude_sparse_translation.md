In this section we want to make `resource.arsc ` file 2X smaller with one line of code.<br/>
If you see inside the ARSC file you will notice that some strings only appear in English but other strings have many translations for them because the Support Library folks went out of their way to localize your strings.<br/>
Multi language app is a good way to reach out more users, but half-translated apps can make a poor user experience. Empty spaces in ARSC file actually use bytes in our ARSC file by indicating no entries. We can simply get rid of this unused languages by adding one line to grade file that we only want english strings.

```gradle
android{
  defaultConfig{
    resConfigs "en"
  }
}

```

This strips away all other string files that could’ve been added by other libraries in languages you don’t even support. To support more language, you can do something similar to this.
```gradle
  defaultConfig { 
  …
  resConfigs “en”, “es”, “ja”, “in” 
  …
}
```


# Results
Here is the result so far on implementing this step.
