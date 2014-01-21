# Getting Started Guide

This guide will walk you through adding Aniways to your app on Android. 
Getting started with Aniways is very easy and takes less than 10 minutes, just follow these short steps to add Aniways to your app:

## Create your Aniways App

First, add new App, and get your App Id.

 > TODO: add screenshot
 
### 1. Download the Aniways SDK

Go to our Download page (under Resources -> Downloads section) and download the latest Android version of Aniways.

 > TODO: link!

The zip file contains 2 folders: a `libs` folder with jar files you need to add to your project and an `AniwaysProject` folder which contains a project with the Aniways resources.

 > TODO: consider renaming this to `AniwaysResourcesProject`

### 2. Add The Aniways project your work set
 
 1. Copy the `AniwaysProject` folder to your workspace.
 2. Import this project into your eclipse workspace (File -> Import -> General -> Existing projects into workspace -> Browse).
 3. Add the Aniways library as an __Android Library Project__ used by your app (Right-click your Android app project -> Properties -> Android -> under "Library" click Add... -> Select Aniways -> OK -> OK).

### 3. Add required libraries to your project

 1. Copy the contents of the `libs` folder to the `libs` folder of your Android App Project. Sometimes a "Refresh" is needed here.
 2. Locate the jars inside this folder in Eclipse and add them to your build path (in Eclipse: Right click -> Build Path -> Add to build path. Then, you need to Right-click your Android App Project -> Properties -> java build path -> order and export tab -> place a __V__ on all the libs you added).

### 4. Init Aniways in your code

Aniways needs to be initialized before any of its components can be used.

This initialization also starts the Aniways service which syncs the phrases and emoticon definitions with the Aniways server.

The initialization needs to be placed in the `onCreate()` method of all entry point activities of the application - the main activity, and any other activity that can start the app flow (for example, by receiving an intent from an external app).

 > TODO: can this be done implicitly?

The init code needs to be placed as close to the beginning of the method as possible.

```java
@Override
public void onCreate(Bundle savedInstanceState){
      Aniways.init(this);    
```

### 5. Replace Your EditText With AniwaysEditText

 > TODO: merge all these (EditText, TextView, ..., ...) together in to a single section.

Aniways inherits from the `EditText` control in which the users type messages and adds capabilities to it.

Therefore, you need to find the layout file where this EditText is defined and replace it with `com.aniways.AniwaysEditText`.

```xml
<com.aniways.AniwaysEditText
   android:id="@+id/chat_input"
   android:layout_weight="1" ...
```

 
### 6. Replace Your TextView With AniwaysTextView

Aniways also inherits from the `TextView` control which is used to display messages on the message wall and adds capabilities to it.

So, you need to find the layout file where the message wall is defined and replace the TextView control/s in it with `com.aniways.AniwaysTextView`.


```xml
<com.aniways.AniwaysTextView
   android:id="@+id/text"
   android:layout_width="wrap_content" ...
```
 
### 7. Converting Icons to text before sending or storing a message

When the user finishes typing a message, your app takes the text from the `EditText` control and then probably performs the following actions:

 * Puts it on the message wall.
 * Sends it to the other side.
 * Stores the message.
 * The `EditText` control returns an `Editable` object which contains Aniways icons in it.

Before doing any of the above actions with the message, you need to first convert the Aniways icons to text using `Aniways.replaceAniwaysIconsWithText()`, so they will not be lost.

Please note that calling `toString()` on the `Editable` removes the Aniways icons altogether, so before calling this method you need to convert the Icons to text codes by calling `Aniways.replaceAniwaysIconsWithText()`.

 > TODO: rename to `Aniways.encodeMessage(Editable)`

```java
private void sendMessage() {
       EditText editView = (EditText) actionWithView.findViewById(R.id.chat_input);
       Editable editableText = editView.getText();
       String text = com.aniways.Aniways.replaceAniwaysIconsWithText(editableText);
       editView.setText("");
       sendMessage(text);
       addMessageToWall(text);
       storeMessage(text);
}
```

### 8. Configure Aniways

Aniways is configured using an xml file.
Please create an `aniways.xml` file under the `res/values` folder.

In order to activate Aniways you need to set the following mandatory configuration parameters:

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
    	
		<!--
		Required: replace placeholder ID with your Aniways App Id
	    -->
		<string name="aniways_appId">Placeholder</string>
	
		<!--
		Required: your App's upgrade URL. Needs to be a url which will redirect to the 
		relevant app store according to device from which it is accessed.
		
		This will be used by users to upgrade to the latest version of your app 
		and be able to see the Aniways Icons inside messages. 
		The ‘http://’ (or https”//) part is essential – please do not use 
		short hands.
	    -->
		<string name="aniways_upgradeUrl">http://www.some_app.com</string>

		<!--
		Sets the short text that will be added to the end of messages and would 
		be visible only to users who do not have the latest version of you 
		app installed.
		
		This message will call upon the user to upgrade to the latest version 
		of the app in order to see the icons inside the message. (the
		users will still receive the Message, but no phrase will be replaced 
		with an icon. The original text would appear instead)
	    -->
	    <string name="aniways_upgradeMessage">
		    This message contains emoticons which you can see after upgrading 
		    to the latest version from:
		</string>
	<resources>


### Optional configuration:

 > TODO: move to the other guids.

There are other configuration properties that you can set which are not mandatory and most apps can just let Aniways use its defaults.

All of these properties are documented in the 'Guides' section on the site, or in the 'Aniways Configuration.docx' file which in the SDK zip file. 

 > TODO: links!!!

### 9. Add permissions in the AndroidManifest.xml file

Add the following permissions to your `AndroidManifest.xml` file (directly under `<manifest>`):

	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.WRITE_INTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.WAKE_LOCK" />
	<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
	<uses-permission android:name="com.android.vending.BILLING" />
	<uses-permission android:name="android.permission.READ_PHONE_STATE" />
	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
	<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

### 10. Add the Aniways services to the AndroidManifest

Aniways uses a service which runs in the background to make sure the application always has the latest version of the phrase definitions and icons. Without the service, Aniways will not function.

Aniways also uses a service to process, cache and send all the analytics data it gathers.

To make the services work, add the following lines to the manifest file (directly under `<application>`)

	<service
		android:name="com.aniways.service.AniwaysIntentService"
		android:process=":AniwaysService" />

	<service
	    android:name="com.aniways.analytics.service.AniwaysAnalyticsService"
        android:process=":AniwaysService" />

	<receiver android:name="com.aniways.service.AlarmReceiver" >
		<intent-filter>
	    	<action android:name="android.intent.action.BOOT_COMPLETED" />
		</intent-filter>
	</receiver>
 
 > TODO: merge into a single service - hide all the details
 
### 11. Test the basic Aniways experiance in your App

Run your app. On the first time, it will synchronize with Aniways server and download all our icons (this is done in the background and can take a minute). Now, when you type words like _coffee_, _pizza_, _burger_, _fries_, _love_, _baby_, _cat_, _tv_, _car_, _star_, the words should be highlighted. When you click on an highlighted word a suggestion popup will be opened and you would be able to replace the word with an icon :)




### 12. Adding other Aniways features to your app

 > TODO: Links to different guides maybe with screenshots (small screenshots)

### 12. Add the Aniways Emoticons on Demand Button

The Aniways Emoticons on Demand Button lets users insert icons without writing text first. The users can browse all the icons by categories, families and recently used.

The icons to choose from are displayed over the keyboard (if it’s opened), or where the keyboard would be when opened (if it’s not currently opened).

There are 3 steps to configure the button:

### 1. Add the button to your layout
 
Place an `ImageView`, or an `ImageButton` where you want the button to be placed in your layout. You can set its size, background color, etc.

### 2. Add Aniways layout placeholder into your layout

Include the aniways_emoticons_button_popup_placeholder layout at the bottom most part of the vertical `LinearLayout` which contains the layout of the activity in which the `AniwaysEditText` is placed. Set the width to `match_parent` and hight to `wrap_content`. This layout has a visibility of `Gone` by default. The idea is that it will be positioned where the keyboard would be when it is opened, and so if the keyboard is not opened, and the button is pressed then Aniways would change its visibility to `Visible` and make it push the `AniwaysEditText` up, like the keyboard would do, and create room for the content of the button to be displayed.

 > TODO: move to FAQ (to configure the displayed images, you will need to change the Aniways resources).
	
	<!— This is the activity layout -->
	<LinearLayout
	    xmlns:android="http://schemas.android.com/apk/res/android"
	    android:id="@+id/chat_activity_root"
	    android:orientation="vertical"
	    android:layout_width="fill_parent"
	    android:layout_height="fill_parent">
	    
	    <!— The chat messages wall -->
	    <ListView />
	    
	    <!— A strip with the EditText and the ‘Send’ and ‘Emoticons’ buttons -->
	    <LinearLayout
	        android:orientation="horizontal"
	        android:layout_width="fill_parent"
	        android:layout_height="wrap_content"
	        android:paddingTop="4dip">
	        
			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
			<!-- Emoticons Button
			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
	        <ImageButton
	            android:id="@+id/emoticons_button"
	            android:layout_width="wrap_content"
	            android:layout_height="fill_parent" />

			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
			<!-- Aniways EditText control
			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
	        <com.aniways.AniwaysEditText
	            android:id="@+id/chat_input"
	            android:layout_weight="1" />


			<!-- Just a button (e.g. "Send") -->
	        <Button
	            android:text="@string/chat_send"
	            android:id="@+id/chat_send"
	            android:layout_width="wrap_content"
	            android:layout_height="fill_parent" />

	    </LinearLayout>
	     
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
		<!-- Aniways layout placeholder
		<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
	    <include
	        android:id="@+id/aniways_emoticons_button_placeholder"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        layout="@layout/aniways_emoticons_button_popup_placeholder" />
	        
	</LinearLayout>

### 3. Initialize the Emoticons button in your code

Init the button to be an Aniways Emoticons Button in the onCreate of the activity which holds it. You need to supply the button creator with the button itself, the EditText to which to add the selected icons, the placeholder and the vertical linear layout which holds the placeholder.

```java
@Override
public void onCreate(Bundle savedInstanceState) {
	// Init Aniways (covered above)?
	
	// Set content view
	setContentView(R.layout.chat_view);
	
	// Setup the button
	LinearLayout activityLayout = (LinearLayout) findViewById(R.id.chat_activity_root);
	LinearLayout aniwaysEmoticonsButtonPlaceholder = 
		(LinearLayout)findViewById(R.id.aniways_emoticons_button_placeholder);
	AniwaysEditText editText = (AniwaysEditText) findViewById(R.id.chat_input);
	ImageView emoticonsButton = (ImageView) findViewById(R.id.emoticons_button);
	
	Aniways.makeAniwaysEmoticonsButton(emoticonsButton, aniwaysEmoticonsButtonPlaceholder, activityLayout, editText);
}
```

Please note that more info on the emoticons on demand button can be found in the “Aniways Emoticons Button Guide.docx” file in the SDK zip.
 
### 12. The Aniways Credits Store (Selling Emoticons)

Aniways lets you lock some of the icons and sell credits that are used to unlock them.

To make the store work, you need to define [in-app managed products in Google Play](http://developer.android.com/google/play/billing/billing_admin.html) for your app. 

These are the credit packs that you would sell. The packs are for 100, 250, 500, 1000, 2000 and 3000 credits. You can define the price for each pack and in each territory in Google Play. To unlock 1 icon the user will need 10 credits, so if he buys the 250 credits pack, for example, then he could unlock 25 icons. Please note that it is preferable to use the default Aniways product ids for the packs, but you can also define your own (the default ids are `aniways_100_credits`, `aniways_250_credits`, `aniways_500_credits`, `aniways_1000_credits`, `aniways_2000_credits`, `aniways_3000_credits`).

After defining the credit packs in the Google Play Developer Console, you need to configure Aniways to use the store and to hook up to your defined products. These are the configuration values that you need to set in the `aniways.xml` file under the ‘values’ folder:

<!-- Whether to enable the Emoticons store. If this is set to 'true' then some of the icons will be locked and the user could unlock them using credits bought on the store. Each icon costs 10 credits. You (the app) decide how much to charge for credits.
There are 6 credit SKUs (product IDs) that you need to define in Google play as !consumable! in-app purchase items: 100, 250, 500, 1000, 2000, 3000 credits.
You decide how much they cost.
For info on how to define the SKUs (product IDs) on Google play, please read: http://developer.android.com/google/play/billing/billing_admin.html 
Please note: When this is set to 'true' then you must also set the SKUs (product IDs) for the credit packages, or this will not work.
Default value is 'true'.
-->
    <bool name="aniways_enable_credits_store">true</bool>
<!-- Should be YOUR APPLICATION'S PUBLIC KEY
(that you got from the Google Play developer console - its in the Services & APIs tab, under 'YOUR LICENSE KEY FOR THIS APPLICATION').
This is not your developer public key, it's the *app-specific* public key.              
Instead of just storing the entire literal string here embedded in the
program,  you can construct the key at runtime from pieces or
use bit manipulation (for example, XOR with some other string) to hide
the actual key.  The key itself is not secret information, but if you don't
want to make it easy for an attacker to replace the public key with one
of their own and then fake messages from the server then you can remove this config
from the XML and instead set it in code in the onCreate() method, just after initializing Aniways.
Default value is: '!!MUST REPLACE THIS with your app's public key'
-->
    <string name="aniways_app_public_key_for_credits_store">!!MUST REPLACE THIS with your app's public key </string>
<!-- The amount of initial store credits to give to the user.
After these credits are spent, the user will need to buy new ones in order to unlock locked icons.
We recommend to use the default value of 100 in order to get the user accustomed to unlocking icons with the credits and increase the chances that he/she will buy more credits when the initial amount is spent.
You need to set this only if the store is enabled.
When the store is enabled, some of the icons will be locked and the user could unlock them using credits bought on the store. Each icon costs 10 credits. You (the app) decide how much to charge for credits.
There are 6 credit SKUs (product IDs) that you need to define in Google play as in-app purchase items: 100, 250, 500, 1000, 2000, 3000 credits.
You decide how much they cost.
For info on how to define the SKUs (product ids) on Google play, please read: http://developer.android.com/google/play/billing/billing_admin.html
Default value is '100'. 
-->
    <integer name="aniways_store_initial_credits">100</integer>
<!-- The SKU (product ID) for 100 credits in the emoticons store.
You need to set this only if the store is enabled.
When the store is enabled, some of the icons will be locked and the user could unlock them using credits bought on the store. Each icon costs 10 credits. You (the app) decide how much to charge for credits.
There are 6 credit SKUs (product IDs) that you need to define in Google play as in-app purchase items: 100, 250, 500, 1000, 2000, 3000 credits.
You decide how much they cost.
For info on how to define the SKUs (product ids) on Google play, please read: http://developer.android.com/google/play/billing/billing_admin.html
Default value is 'aniways_100_credits'. 
-->
<string name="aniways_100_credits_sku">aniways_100_credits</string>    
<!-- The SKU (product ID) for 250 credits in the emoticons store. -->
<string name="aniways_250_credits_sku">aniways_250_credits</string>
<!-- The SKU (product ID) for 500 credits in the emoticons store. -->
<string name="aniways_500_credits_sku">aniways_500_credits</string>
<!-- The SKU (product ID) for 1000 credits in the emoticons store. -->
<string name="aniways_1000_credits_sku">aniways_1000_credits</string>
<!-- The SKU (product ID) for 2000 credits in the emoticons store. -->
<string name="aniways_2000_credits_sku">aniways_2000_credits</string>
<!-- The SKU (product ID) for 3000 credits in the emoticons store. -->
<string name="aniways_3000_credits_sku">aniways_3000_credits</string>
 
 
### ??  Add the Aniways Credits Store Activity to the App Manifest:

Add the following lines to the manifest file (directly under <application>)

products. These are the configuration values that you need to set in the ‘aniways.xml’ file under the ‘values’ folder:


	<activity 
		android:name="com.aniways.billing.AniwaysCreditsStoreActivity" 		
		android:theme="@style/Theme.Aniways.Transparent" 
		android:launchMode="singleTop" />

Please note that more info on the credits store can be found in the “Aniways Credits Store Guide.docx” file in the SDK zip.

 
