# Mac AppStore patch for node-webkit
This patch is totally based on this work: https://github.com/rogerwang/chromium.src/pull/17

The original patch by @trevorlinton did not work with 0.11.5, so fixed it for the newer version until node-webkit official repository gets updated with the proper changes and buildbot for Mac AppStore file.

## Background

node-webkit executable cannot be submitted to Mac AppStore as is and needs to be tweaked; this patch removes usage of QuickTime libraries and makes a few other changes that allow node-webkit to be submitted to AppStore.

It is further discussed here: https://github.com/rogerwang/node-webkit/issues/936
