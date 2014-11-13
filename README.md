# BRNImagePickerSheet

## About
BRNImagePickerSheet is a duplicate of that shiny new custom action sheet seen in iOS8's iMessage that Apple didn't make part of UIKit. It's the first project I've written in Swift. It works well but I might have coded something the Objective-C kind of way. Don't hesitate to open an issue/ pullrequest if you spotted something.

![BackgroundImage](https://raw.github.com/larcus94/BRNImagePickerSheet/master/Screenshots/BRNImagePickerSheet-about.png)
![BackgroundImage](https://raw.github.com/larcus94/BRNImagePickerSheet/master/Screenshots/BRNImagePickerSheet-about-selected.png)

## Author
I'm Laurin Brandner, I'm on [Twitter](https://twitter.com/larcus94).

## Usage
BRNImagePickerSheet's API is similar to the one of UIActionSheet so you should get along with it just well.

### Example

```swift
let placeholder = BRNImagePickerSheet.selectedPhotoCountPlaceholder
var sheet = BRNImagePickerSheet()
sheet.numberOfButtons = 3
sheet.delegate = self
sheet.showInView(self.view)
```

```swift
func imagePickerSheet(imagePickerSheet: BRNImagePickerSheet, titleForButtonAtIndex buttonIndex: Int) -> String {
    let photosSelected = (imagePickerSheet.selectedPhotos.count > 0)

    if (buttonIndex == 0) {
        if photosSelected {
            return NSLocalizedString("Add comment", comment: "Add comment")
        }
        else {
            return NSLocalizedString("Take Photo Or Video", comment: "Take Photo Or Video")
        }
    }
    else {
        if photosSelected {
            return NSString.localizedStringWithFormat(NSLocalizedString("BRNImagePickerSheet.button1.Send %lu Photo", comment: "The secondary title of the image picker sheet to send the photos"), imagePickerSheet.selectedPhotos.count)
        }
        else {
            return NSLocalizedString("Photo Library", comment: "Photo Library")
        }
    }
}

func imagePickerSheet(imagePickerSheet: BRNImagePickerSheet, willDismissWithButtonIndex buttonIndex: Int) {
    if buttonIndex != imagePickerSheet.cancelButtonIndex {
        if imagePickerSheet.selectedPhotos.count > 0 {
                println(imagePickerSheet.selectedPhotos)
        }
        else {
            let controller = UIImagePickerController()
            controller.delegate = self
            controller.sourceType = (buttonIndex == 2) ? .PhotoLibrary : .Camera
            self.presentViewController(controller, animated: true, completion: nil)
            }
        }
    }
}
```
BRNImagePickerSheet uses a delegate method, similar to UITableView's dataSource, to get the title of a button. In conjunction with [stringsdict](https://developer.apple.com/library/ios/documentation/MacOSX/Conceptual/BPInternational/StringsdictFileFormat/StringsdictFileFormat.html), this allows for easy translation of various plural forms.

## Installation

BRNImagePickerSheet will be available via [CocoaPods](http://cocoapods.org). However there's an [issue](https://github.com/CocoaPods/CocoaPods/issues/2226) with Swift compatibility that caused the build to fail. I will release it as soon as possible though.

<!---
BRNImagePickerSheet is available via [CocoaPods](http://cocoapods.org).

To install add the following line to your Podfile:

    pod 'BRNImagePickerSheet'

-->

(There is apparently an issue with Xcode6 and Swift static libs. Check out [this issue](https://github.com/CocoaPods/CocoaPods/issues/2226) for more.

## Requirements
BRNImagePickerSheet is written in Swift and links agains `Photos.framework`. It therefore requires iOS 8 or later.

## License
BRNImagePickerSheet is licensed under the [MIT License](http://opensource.org/licenses/mit-license.php).
