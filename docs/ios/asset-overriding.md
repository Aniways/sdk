### Customization of the Keyboard Segmented Control

 > TODO: 

You can customize the appearance of the segmented control (categories control) 
by overriding the Aniways asset files which are located under the 
Resources directory (Aniways.embeddedframeword -> Resources).

 > TODO: Maybe not true? maybe just add those resources with the proper name
   and then they will override the ones in the framework.

All you need to do is create your own version of these resources, keep the 
same name and save it in the same location. Please avoid resizing the 
resources, this may results with unexpected results.

If you decide to change a resource file, don’t forget to override both 
retina (@2x) and non-retina resources.

Here are the resources that effect the Aniways keyboard appearance:

 * `aniways_ebp_bg_n_tab.png`: segmented control background in normal state
 * `aniways_ebp_bg_s_tab.png`: segmented control background in selected state
 * `aniways_ebp_bg_seperator.png`: segmented control separator

Categories appearance:

 * `n_aniways_ebp_<category name>_button.png` – category image in normal state
 * `s_aniways_ebp_<category name>_button.png` – category image in selected state


### Store Asset Customization

You can change the look and feel of all store elements in such a way that it will best feet your app's appearance.

You can customize the appearance of the all store elements by changing and overriding their resource which are located under the Resources directory (Aniways.embeddedframeword -> Resources).

All you need to do is to create your own version of the resources, keep the same name and save it in the same location. Please avoid from resizing the resources, this may results with unexpected results.

Don’t forget to override both retina (@2x) and non-retina png files.

Here are the resources that effect the store appearance:

 - `coin_lock.png` – locker and price image which appears on a locked icon 
   (__restrictions__: price must remains 10 credits).
 - `popup_coins_balance.png` - image which contains the user credit balance, 
   both in the icons keyboard and popup (__restrictions__: the position and size of the label that contains the balance text cannot be changed).

 > TODO: (in 2017) - maybe separate to two assets?

 - `store_portrait_bg.png` - the background image of the credits store in 
   portrait mode (__restrictions__: the position and size of the label that contains the balance text cannot be changed)

  - `store_landscape_bg.png` - the background image of the cresits store in 
    landscape mode (__restrictions__: the position and size of the label that contains the balance text cannot be changed)

  - `coins.<number of coins>.png` - product container image (__restrictions__: credits number should not be changed, the position and size of the bottom label that contains the price text cannot be changed)

  - `store_x.png` - the x button for closing the store.

  - `cash_register.m4a` - voice that being played upon credit purchase
  - `unlock.m4a` - voice that being played upon unlocking an icon


customize
You can change the “look & feel” of the tutorial in such a way that It will best feet your app appearance.

You can customize the appearance of the all store elements by changing and overriding their resource which are located under the Resources directory (Aniways.embeddedframeword -> Resources).

All you need to do is to create your own version of the resources, keep the same name and save it in the same location. Please avoid from resizing the resources, this may results with unexpected results.

Don’t forget to override both retina  (@2x) and non-retina png files.

tutorial_bottom_left – tutoril tap instruction where it is located below and point to the left (restrictions: arrow should point to the upper left corner).
tutorial_bottom_right – tutoril tap instruction where it is located below and point to the right (restrictions: arrow should point to the upper right corner).
tutorial_top_left –tutoril tap instruction where it is located above and point to the left (restrictions: arrow should point to the bottom left corner).
tutorial_top_right – tutoril tap instruction where it is located above and point to the right (restrictions: arrow should point to the bottom right corner).

