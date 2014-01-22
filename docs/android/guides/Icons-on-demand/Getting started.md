# Quick setup of the Aniways Emoticons on Demand Button

This guide will walk you through adding the Aniways Emoticons on demnd button to your app.

The Aniways Icons on Demand Button lets users insert icons without writing text first. The users can browse all the icons by categories, families and recently used.
The icons to choose from are displayed over the keyboard (if it’s opened), or where the keyboard would be when opened (if it’s not currently opened).

The guide assumes that you have already performed the actions described in the [getting started guide] (https://github.com/Aniways/sdk/blob/master/docs/android/Getting%20started.md)

## 1. Add the button to your layout
 
Place an `ImageView`, or an `ImageButton` where you want the button to be placed in your layout. You can set its size, background color, etc.

## 2. Add Aniways layout placeholder into your layout

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

## 3. Initialize the Emoticons button in your code

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

 > Please note: that more info on the emoticons on demand button can be found in the Aniways emoticons on demnd Guide.
