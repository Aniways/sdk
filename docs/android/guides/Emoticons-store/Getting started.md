# Quick setup of the Aniways Emoticons Store

This guide will walk you through adding the Aniways Emoticons Store to your app.

The store lets you lock some of the icons we provide and sell credits that are used to unlock them.

The guide assumes that you have already performed the actions described in the [getting started guide] (https://github.com/Aniways/sdk/blob/master/docs/android/Getting%20started.md)

## 1. Define in-app products in Google Play

To make the store work, you need to define [in-app managed products in Google Play](http://developer.android.com/google/play/billing/billing_admin.html) for your app. 

These are the credit packs that you would sell. The packs are for 100, 250, 500, 1000, 2000 and 3000 credits. You can define the price for each pack and in each territory in Google Play. To unlock 1 icon the user will need 10 credits, so if he buys the 250 credits pack, for example, then he could unlock 25 icons. Please note that it is preferable to use the default Aniways product ids for the packs, but you can also define your own (the default ids are `aniways_100_credits`, `aniways_250_credits`, `aniways_500_credits`, `aniways_1000_credits`, `aniways_2000_credits`, `aniways_3000_credits`).

After defining the credit packs in the Google Play Developer Console, you need to configure Aniways to use the store and to hook up to your defined products. These are the configuration values that you need to set in the `aniways.xml` file under the ‘values’ folder:

	<!-- Whether to enable the Emoticons store. If this is set to 'true' then some of the icons will be locked and 	             the user could unlock them using credits bought on the store. Each icon costs 10 credits. You (the app)                 decide how much to charge for credits.
	     There are 6 credit SKUs (product IDs) that you need to define in Google play as !consumable! in-app 		     purchase items: 100, 250, 500, 1000, 2000, 3000 credits.
	     You decide how much they cost.
	     For info on how to define the SKUs (product IDs) on Google play, please read: 	  
	     http://developer.android.com/google/play/billing/billing_admin.html 
	     Please note: When this is set to 'true' then you must also set the SKUs (product IDs) for the credit 	             packages, or this will not work.
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
 
## 2.  Add the Aniways Credits Store Activity to the App Manifest:

Add the following lines to the manifest file (directly under <application>)

products. These are the configuration values that you need to set in the ‘aniways.xml’ file under the ‘values’ folder:


	<activity 
		android:name="com.aniways.billing.AniwaysCreditsStoreActivity" 		
		android:theme="@style/Theme.Aniways.Transparent" 
		android:launchMode="singleTop" />

Please note that more info on the credits store can be found in the “Aniways Credits Store Guide.docx” file in the SDK zip.
