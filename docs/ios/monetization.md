# Monetization

This guide will walk you through configuring the Aniways credits store in 
your iOS app. The store lets you lock some of the icons and sell credits that are used to unlock them.

Locked icon looks as follow:

 > TODO: IMAGE

When the user has enough credits to unlock an icon (10 credits) then the 
icon will be unlocked and placed inside the message.

If the user doesn’t have enough credits to unlock an icon and they
click on it, then the store opens:

 > TODO: IMAGE

Users can also access the store if they click on the credits balance.

 > TODO: IMAGE

In the store the user can purchase more credits using Apple In-App Purchase mechanism.

### 1. Define In-App Purchase Products in iTunes Connect

 1. Log into [iTunes Connect](https://itunesconnect.apple.com). 
 2. On the Home page, click __Manage Your Apps__.
 3. Click on the app for which you wish to create an __In-App Purchase__
 4. On the App Summary page, click __Manage In-App Purchases__

  > TODO: Add links!

  > Note: If you do not see the __Manage In-App Purchases__ button, you may not have the latest __Paid Applications Contract__ signed, or your team agent did not agree to the latest __iOS Developer Program__ or __Mac Developer Program__ license agreement. If you still do not see the button, contact __iTunes Connect Support__ using the __Contact Us__ module on the iTunes Connect homepage.

 5. Define the following products:

    `<your app bundle id>.coins.100`
    `<your app bundle id>.coins.250`
    `<your app bundle id>.coins.500`
    `<your app bundle id>.coins.1000`
    `<your app bundle id>.coins.2000`
    `<your app bundle id>.coins.3000`

  Follow these steps:

  * Click __Create New__ 
  * Click __Select__ in the __Consumable__ section.
  * Fill in the following production information:

__Reference Name__: Common name for the product - X coins

__Product ID__: <your app bundle id>.coins.<coins number>.

__Price Tier__: price of the product. See the price matrix for the different tiers.

__Language to Add__: Pick one. 

The following two fields will appear:

__Displayed Name__: 100/250/500/1000/2000/3000 coins

__Description__: Credits of 100/250/500/... coins

__Screenshot__: Your feature in action. 

 > NOTE: Despite the text on the screen about the screenshot submission triggering the product review process (a very sloppy design choice, IMHO), you can safely add the screenshot now without the product being submitted for review. After saving the product, just choose the “Submit with app binary” option. This will tie the product to the app binary, so when you finally submit the 100% complete app binary, the product will be submitted as well.

  * Click __Save__.

Your In-App purchase can now be viewed on the __Manage In-App Purchases__ page for your app.

### 2. Aniways Configuration

 * `EnableStoreService` should be `YES`
 * `InitialCreditsForUser` should include the initial number of credits each
   user receives when they first install the app. For example, `100`.

 > TODO: rename all configuration to `AWxxx` and move to `Info.plist`.
