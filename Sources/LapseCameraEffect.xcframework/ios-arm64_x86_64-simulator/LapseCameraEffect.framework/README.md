# Lapse Camera Effect

Usage:

```
let effect: DistortEffect

init() {
  effect = DistortEffect()
}

func run(pixelBuffer: CVPixelBuffer) {

  let config = EffectConfiguration(aberration: Aberration(red: 0.0, green: 0.0, blue: 0.0), blur: 0.0, distortion: 0.0)

  let newPixelBuffer = effect.apply(pixelBuffer: pixelBuffer, with: config)

}
```



# XCFrameworks

https://www.appcoda.com/xcframework/

# Archive for device
```
xcodebuild archive -scheme LapseCameraEffect -destination="iOS" -archivePath /tmp/xcf/ios.xcarchive -derivedDataPath /tmp/iphoneos -sdk iphoneos SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES BUILD_LIBRARY_FOR_DISTRIBUTION=YES
```


# Archive for simulator
```
xcodebuild archive -scheme LapseCameraEffect -destination="iOS Simulator" -archivePath /tmp/xcf/iossimulator.xcarchive -derivedDataPath /tmp/iphoneos -sdk iphonesimulator SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES BUILD_LIBRARY_FOR_DISTRIBUTION=YES
```

# Build XCFramework

```
xcodebuild -create-xcframework -framework /tmp/xcf/ios.xcarchive/Products/Library/Frameworks/LapseCameraEffect.framework -framework /tmp/xcf/iossimulator.xcarchive/Products/Library/Frameworks/LapseCameraEffect.framework -output /tmp/xcf/LapseCameraEffect.xcframework
```

# Test Locally

- [ ] Close Xcode, Yes, Close Xcode
- [ ] Re-open Xcode
- [ ] Drag the whole swift package folder onto the project you want to add it to
- [ ] Go to the general tab
- [ ] Frameworks, Libraries & Embedded Content
- [ ] Click + 
- [ ] Select the Package

# Packaging up

- [ ] Delete all sources, and copy LapseFilter.xcframework directly under sources

```
// swift-tools-version:5.3
// The swift-tools-version declares the minimum version of Swift required to build this package.

import PackageDescription

let package = Package(
    name: "LapseCameraEffectPackage",
    products: [
        // Products define the executables and libraries a package produces, and make them visible to other packages.
        .library(
            name: "LapseCameraEffectPackage",
            targets: ["LapseCameraEffect"]),
    ],
    dependencies: [
        // Dependencies declare other packages that this package depends on.
        // .package(url: /* package url */, from: "1.0.0"),
    ],
    targets: [
        .binaryTarget(name: "LapseCameraEffect", path: "./Sources/LapseCameraEffect.xcframework")
    ]
)

```
