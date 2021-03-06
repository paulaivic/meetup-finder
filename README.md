#Meetup-finder

This is an iOS demo app that helps find when and where the upcoming technology meetups are happening near the user’s current location, using the [meetup.com API] (https://secure.meetup.com/meetup_api).

<img src="/screenshots/screenshot-2.png" width="213px" height="380px" />&nbsp;&nbsp;
<img src="/screenshots/screenshot-3.png" width="213px" height="380px" />&nbsp;&nbsp;
<img src="/screenshots/screenshot-4.png" width="213px" height="380px" />

## Specs
- Swift 2.0
- iOS 9 compatible
- Created using Xcode 7

## Features
1. Meetup-finder allows users to see the list of upcoming technology meetups around their area by just launching the app.
2. Users can locate and browse the venue locations using the Map View.
3. More detailed information about the event is provided to the users when an event is selected.
4. Users are able to add the event into their iCloud Calendar from the Event Information View `EventDetailsViewController.swift`.

## Peek and Pop on 3D Touch-capable devices 
### (iPhone 6S and iPhone 6S Plus)
Meetup-finder provides Peek and Pop functionality to preview additional content when a user presses (3D Touch) on any item of the list of meetups. See `NearMeViewController.swift` and `PreviewViewController.swift`

``` bash
func registerFor3DTouch(){
  //Register view for 3D Touch (if available)
  if traitCollection.forceTouchCapability == .Available {
    registerForPreviewingWithDelegate(self, sourceView: self.tableView)
  } else { 
    print("3D Touch is not available on this device.") 
  }
}
end
```

## Getting Started
1. Clone/Download the repository.
2. Open the project in Xcode `Meetup Finder.xcworkspace`.
3. Open `config.plist` and set your Meetup.com API Key in `wsAPIKey`. This key is required to make every request to the Meetup API. You can see your API Key [here](https://secure.meetup.com/meetup_api/key/).
4. Build and run the app.

## API methods implemented
1. [/topics] (http://www.meetup.com/meetup_api/docs/topics/) to get all the "Tech" related topics. The `urlkeys` in the response are being sent as a parameter when requesting the meetups.
2. [/2/open_events] (http://www.meetup.com/meetup_api/docs/2/open_events/) to get all the upcoming public events hosted by Meetup groups.
3. [/2/groups] (http://www.meetup.com/meetup_api/docs/2/groups/) to get detailed information about the Meetup groups.

## Third-party frameworks/libraries 
Third-party open source framewors are used within this project:

1. [RestKit](https://github.com/RestKit/RestKit) - For consuming and modeling RESTful web resources
2. [SDWebImage](https://github.com/rs/SDWebImage) - Asynchronous image downloader with cache support***

Installed via the [CocoaPods](http://cocoapods.org/) dependency management tool, as it makes managing dependencies in the code easier.

``` bash
platform :ios, '8.4'

target 'Meetup Finder' do

pod 'RestKit', '~>  0.24.1'
pod 'SDWebImage', '~> 3.7'

end
```
Since this is a Swift project and these frameworks were created in Objective-C, a bridging header was added to expose the headers to Swift: `Meetup Finder-Bridging-Header.h`.

##Notes/Updates

***To display/download Meetup.com's group photos - UPDATE: This feature was removed from the app to avoid the credentials to get blocked. Meetup.com allows only a maximum number of requests that can be made in a time frame. Clients that issue too many requests in a short period of time will be blocked for an hour. However, the implementation to request the group photos was kept in the class `DataManager.swift`.
