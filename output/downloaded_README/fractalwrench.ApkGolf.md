# ApkGolf
This repository hosts the smallest Android APK in the world. The current size of the APK is *678 bytes*.

To learn more about how this was achieved, please read the [blog post](https://fractalwrench.co.uk/posts/playing-apk-golf-how-low-can-an-android-app-go/).

If you have beaten my score at APK Golf, please submit a PR, and I'll happily add you to the hall of fame!


# Hall of Fame

## Using DSA Keystore, reducing manifest size (1295 bytes, 26% reduction)
The manifest can be further optimised by using a compiled XML file instead, and a DSA Keystore is smaller than the default generated by Android Studio.

Contributed by [Madis Pink](https://github.com/madisp) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/3)

## Insane zopfli compression (1180 bytes, 9% reduction)
This improves compression of the APK.

Contributed by [Gautam Korlam](https://github.com/kageiit) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/5)

## Use Elliptic-curve signatures (922 bytes, 16% reduction)
Elliptic-curve signatures are even smaller than DSA, and are supported in APK v2 signing.

Contributed by [Robert Xiao](https://github.com/nneonneo) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/4)

## Remove classes.dex (824 bytes, 11% reduction)
If a code element is not present in the manifest, no classes.dex file is required by the `PackageParser`.

Contributed by [Robert Xiao](https://github.com/nneonneo) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/12)
Original idea from [zhuowei](https://github.com/zhuowei), raised in this [Issue](https://github.com/fractalwrench/ApkGolf/issues/8)

## Further hand tuning of manifest (820 bytes, 0.5% reduction)
Further byte-level optimisation of what remains of the manifest.

Contributed by [Madis Pink](https://github.com/madisp) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/6)

## Minimising APK Signing Certificate (678 bytes, 18% reduction)
Manual removal of unnecessary fields present in the certificate used to sign the APK.

Contributed by [klyubin](https://github.com/klyubin) in this [Pull Request](https://github.com/fractalwrench/ApkGolf/pull/15)
