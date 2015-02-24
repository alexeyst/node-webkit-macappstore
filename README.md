# Mac AppStore patch for node-webkit
This patch is totally based on this work: https://github.com/rogerwang/chromium.src/pull/17

The original patch by @trevorlinton did not work with 0.11.5, so I fixed it for the newer version until node-webkit (or now nw) official repository gets updated with the proper changes, and buildbot slave is created for Mac AppStore executable.

## Background

node-webkit (now nw.js) executable cannot be submitted to Mac AppStore as is and needs to be tweaked is its Chromium part uses QuickTime and various deprecated / private APIs; this patch removes usage of QuickTime libraries and makes a few other changes that allow node-webkit to be submitted to AppStore. The binary from this repository was successfully submitted via Application Loader on Jan 14th, 2015.

It is further discussed here: https://github.com/rogerwang/node-webkit/issues/936

## Important Update

Latest review in January required to drop some more APIs, so I also had to patch the webkit located within `node-webkit/src/third_party/WebKit` to get it approved by App Store.

## How to get node-webkit build accepted on Mac App Store
I figured out that Apple may be rejecting the latest ffmpegsumo.so located under libraries. If you do not use ffmpeg, you may delete the file from `node-webkit Framework.framework/Libraries/ffmpegsumo.so` and resubmit. 

If you do use ffmpeg, however, more investigations are necessary to submit it to App Store—it uses certain QtKit APIs that need removal as well (or rather, a conversion to AVFoundation).

The most recent binary of 0.11.5 was accepted by App Store without ffmpegsumo.so on January 26th 2015 (and once with it, too, earlier).

### Submitting to App Store

To ensure successful submittion, you will need to:

1. Delete the `ffmpegsumo.so` (if you're not using it, as explained above)
* Edit the plist to match your app ID
* Sign the code with the right entitlements that enable sandbox on it [see here by @trevorlinton](https://www.trueinteractions.com/macstore_sign.sh)
* Ensure you do not request the entitlements you do not need (like printing or etc., App Review team checks that)
* Finally, create a package with productbuild tool on your Mac and upload to App Store for review.

### Sandboxing Issues

Once sandboxed, the app may crash with `deny forbidden-sandbox-reinit` error. To fix that, please see this [closed issue](https://github.com/alexeyst/node-webkit-macappstore/issues/1) for details.
