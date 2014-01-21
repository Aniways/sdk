# Emoticon Keyboard

This guide describes how to add and setup the Aniways Keyboard within 
your iOS app. 

The Aniways Emoticons Keyboard lets users insert icons on demand (without replacing part of the text). 
The users can browse all the icons by categories and families.

The first tab is the __Genius__ tab which contains all the recently used 
icons combined with relevant icons based on the text that is written in 
the textview. 

In the following example you can see that the icons that are being 
suggested in the genius category related to the text that is written.

 > TODO: IMAGE

Aniways provides an `AniwaysIconOnDemandButton` class which inherits 
from `UIButton` and adds capabilities to it. Therefore, all you need to do 
is to create such a button (either via code or in your NIB or storyboard), 
place it in your desired location, design it and set the 
`AniwaysTextView` in its `textView` property.

 > TODO: Rename to `AWKeyboardButton`

```objc
AniwaysIconOnDemandButton* iconButton = [[AniwaysIconOnDemandButton alloc] initWithFrame:frame];
iconButton.textview = myAniwaysTextView; // <-- required
```

Clicking on your button will switch back and forth between the original 
keyboard and the Aniways keyboard.

## Keyboard Customizations

The Aniways keyboard supports the following customization settings:

 * `AWIconsKeyboardBackgroungColor` – the background CSS color of the 
   icons keyboard view (e.g. `#cccccc`)
 * `AWRecentlyUsedLimitNumber` – the maximum number of recently used icons
   that will be presented as part of the __recently used__ category.
 * `AWKeyboardIconSize` – size of icons when appearing inside the keyboard view. 
   The number of icons in each page is automatically calculated based upon 
   the icon size.

 > NOTE: In order to change configuration parameters please open 
   the `AniwaysConfiguration.plist` file which is located under the resources 
   directory. 

 > TODO: change to read from `Info.plist`