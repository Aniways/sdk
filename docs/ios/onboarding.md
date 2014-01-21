# Aniways Onboarding Experience

This guide will walk you through configuring Aniways tutorial in your iOS app.
The tutorial explain the users how to interact with aniways highlighted keywords.
On the first X times (configurable number) that a highlighted keyword is written the screen is freezed and the user is being introduced to the highlighted keyword and the way to interact with it:

 > TODO: IMAGE

When the user taps the highlighted keyword the suggestion popup will be opened:

 > TODO: IMAGE

Otherwise he can always close the tutorial by cklicking on the x button.

In order to activate the tutorial feature you need to set a number which is bigger than `0` to the `MaxTimesToShowTutorial` configuration parameter.

 > Move to `Info.plist` and rename to `AWMaxTimesToShowTutorial`.
 