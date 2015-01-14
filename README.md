# Mac AppStore patch for node-webkit
This patch is totally based on this work: https://github.com/rogerwang/chromium.src/pull/17

The original patch by @trevorlinton did not work with 0.11.5, so I fixed it for the newer version until node-webkit (or now nw) official repository gets updated with the proper changes, and buildbot slave is created for Mac AppStore executable.

## Background

node-webkit (now nw.js) executable cannot be submitted to Mac AppStore as is and needs to be tweaked is its Chromium part uses QuickTime and various deprecated / private APIs; this patch removes usage of QuickTime libraries and makes a few other changes that allow node-webkit to be submitted to AppStore. The binary from this repository was successfully submitted via Application Loader on Jan 14th, 2015.

It is further discussed here: https://github.com/rogerwang/node-webkit/issues/936
