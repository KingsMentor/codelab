There are things to really care about for the success of your app. Apk size happens to be one of them. It's important to keep apk as small as possible to avoild been preyed when the user goes hunting for memory space. <br>
This codelab covers:<br>
* Series of Best practices on how to reduce your apk size (Tools and Features to help you achieve this)

## Dimensions of APK Size
We all know why the application size is very important. APK size can be looked at two dimension. 
1. **Download Size** - It is size of the application in the Play Store and it gets delivered to the device. This size is highly compressed.
2. **Installed size** - Installed size is when you download the app and unpack it. Install size is two to three times bigger than the download size.<br/></br>
![dimersions of apk size](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/apk_dimensions.jpeg)  

## Analysing Apk Size
`Android studio 3.0` came with a whole lot of upgrade. Amongst which is `Analyze Apk`. This feature allows you analyse apk, showing resources in your apk and how it contribute to the final apk size. This is a great resource on focusing on resources that contribute large data to your final apk.

![dimersions of apk size](https://raw.githubusercontent.com/KingsMentor/codelab/master/buildingsmallerapk/imgs/apk_dimensions.jpeg)  


Notice that there are two columns with size information. 

1. **Raw file size** - The Raw file size is how much every particular item contribute to the size of APK as a file on disk.
2. **Download size** - The second is download size which represent how much bytes the user will actually have to download from Play Store on order to install the app for the first time

As you can see, `libs` (dependencies being used on this project) contribute about `20mb` to the final size and for `resources` these numbers aren’t very far apart because resources are dominated bye large PNG we have for drawables and can’t be further compressed. Whereas for some other items the gains from compression are higher. 

Next, I am going to show a how a bunch of tricks and their impact on app size. I will be runing through series of best pratices and analysing the output apk at every point in time.

<aside class="special"><p>There is an important point that optimizing your own app size begins with sort of finding out what’s in it and tailoring to that.<b>Your milage may vary</b> .</p></aside>
