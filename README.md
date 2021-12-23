# GDIChromium
> GDI font rendering re-implementation for Chromium, which looks much better than DirectWrite.
> Allowing a seamless usage of Font substitution applications such as [MacType](https://github.com/snowie2000/mactype).

<br/>
<p align="center">
    <img src="https://user-images.githubusercontent.com/25143912/136350008-42fba9a0-9511-46fb-8f43-6db57dd76bc6.png" width="500px"/>
</p>

## Note
The binaries are provided for demonstrative purposes and should not be compared to full-featured browsers, the minimalistic approach of keeping it clear of additional features is intended. If you are only looking to disable direct write, the binaries will make you happy and will avoid you from wasting a lot of time on slightly complex chromium compilation process. it takes 2-4 hours on a server with 2x E5-2690v2 to compile the binaries, not to mention cloning the +20GB repository and getting the flags correctly set up. 

The sole purpose of using these patches/this browser is for it to be used in combination with MacType or alternative. 
Let me rephrase and simplify, the fonts will look horrible without using MacType. don't say I didn't warn you! :)

## Synopsis
On Windows, Google Chrome has supported two standards for font rendering. Font rendering is the actual process that leads to display text on our screens. One of the font rendering modes is called GDI, the other is DirectWrite. DirectWrite is default since version 37 (released in 2014). Since then Google has offered disabling it in case someone wanted to use GDI instead. This could be done by enabling the flag #disable-direct-write at chrome://flags. When DirectWrite was disabled, Chrome used the GDI rendering.

Why was this good and why did a lot of us want to disable DirectWrite? A font that appears on the screen has to be smoothed/anti-aliased. This is the point where the two standards differ and the difference is significant. DirectWrite anti-aliases much less readable fonts than the original good old GDI. So the answer is simple: A lot of us wanted to disable DirectWrite because GDI produces much sharper and more readable fonts.

## Motivation
Unfortunately, GDI support has been removed in order to save some development effort. This change has already reached the frontline of Chrome releases, so sooner or later everyone of us will face less readable, blurry fonts, whether we want or not. Developers with this decision are taking away the free choice between GDI and DirectWrite, between sharp and blurry fonts. In addition, blurry fonts of DirectWrite cause headache, nausea at a lot of people, including me.

## Full story and technical background

A long time ago, two developers, namely Ilya Kulshin and Scott Graham created patches that would remove support for GDI font rendering completely from the Chromium codebase.

https://codereview.chromium.org/1919573002

https://bugs.chromium.org/p/chromium/issues/detail?id=579678

https://chromium.googlesource.com/chromium/src/+/1acd6b6af8c9ef59fe7227faff4585310e5c2ec8

They've done this without any direct consent from users and with a reason like since we have already sorted out support for XP/Vista, we don't need GDI anymore. They've done this despite the fact that a lot of users wanted to get rid of DirectWrite after it became default in the stable releases of Chromium and Chrome (around version 37). They've done this despite the fact that GDI is still fully supported in Windows 7 which was the most widely-used (and also the most mature, most stable) Windows. Windows 7 is no longer officially supported by Microsoft, but still a lot of users do really want to take advantage of different rendering techniques. As a consequence, GDI is also officially supported by Microsoft as it's part of the operating system. Thus, GDI rendering is also supposed to be supported and offered as a choice like any other platform-specific settings in Chromium. Furthermore, DirectWrite is incapable of giving the same look and feel as GDI, as you don't need glasses to see this in the comparison above. For those who prefer grayscale anti-aliasing, this means a serious degradation in quality and readability. Of course you can turn on ClearType, however there are people like me (even if we are a minority) who do not prefer ClearType and any kind of sub-pixel rendering. ClearType uses sub-pixels for smoothing font edges which is basically violating the original purpose of sub-pixels and by this it pollutes the color space that results in color fringes and bleeding. There are many displays with different (mostly lower) contrast ratios on which you simply can't tune ClearType well, it will always bleed or have noticeable color fringes. Also, for notebooks used with different backlight brightness levels (day/night) sometimes there is no universal settings without noticeable bleeding or color fringes. Even though the ClearType rendering of GDI is poorer than of DirectWrite, at grayscale rendering the winner is definitely GDI and it has done a really good job for several years: sharp, well-hinted fonts and even sharper edges (even sharper than DirectWrite with ClearType on).

### Acknowledgments
https://www.change.org/p/google-inc-bring-sharp-fonts-back-in-google-chrome-disable-directwrite


## How to install
1. Download the [latest version](https://github.com/GTANAdam/GDIChromium/releases)
2. Launch the executable and wait a little bit
3. Launch "Chromium" from your desktop

## Upgrading from CentBrowser
For those wishing to just seamless upgrade from CentBrowser, follow the instructions:

1. Make sure CentBrowser and GDIChromium are not running
2. Navigate to ``%LocalAppData%``
3. Remove "User Data" folder inside Chromium
4. Copy "User Data" folder inside CentBrowser to Chromium
5. Launch the new browser and voila! your stuff are there!
