## Overview
This guide explains the newly adopted convention for using colors in oppia-android and adding support for dark mode 
to any particular layout while keeping the code organised and strictly following the decided convention.

The approach is to split color declarations in 4 different files instead of keeping the colors at one place, promoting separations of 
concerns and hence improving code maintainability and understandibility.



##### Knowing the convention

The following files have been added for maintaining the colors : 
1. **`color_defs.xml`**<br>
	 This file should strictly contain actual color names (irrespective of their intended use) with their hex color code declaration.<br>
	 example:<br>
	 ```xml
	 <color name="lime_green">#90EE90</color>
	 <color name="blue">#0000FF</color>
	 ```
	 Declarations from this file should be only used in `color_palette.xml`.

2. **`color_palette.xml`**<br>
	There are two versions for this file (day/night variations). The purpose of this file is to split the colors for them to be later referenced by `component_colors.xml`. The color declarations in this should have a generic name and should not contain any name tied to the intended component to be used on.
	The declarations in this file should only reference `color_defs.xml`.
	>Don't:
	```xml
 	<color name="add_profile_background_color">@color/light_black</color>
 	<color name="text_input_layout_error_color">@color/oppia_pink</color>
	```
	>Do:
	```xml
 	<color name="background_color">@color/light_black</color>
 	<color name="error_color">@color/oppia_pink</color>
	```
	You can refer to both variations of these files to see how it separates the colors.
3. **`component_colors.xml`**<br>
	This file contains the highest level of color declarations. The declarations in this file should only reference `color_palette.xml`. It uses UI component specific names. Component colors should be shared very little outside of their respective views/fragments/activities. *All the layouts/views should only reference this file for colors.*<br>
	examples:<br>
	```xml
 	<color name="shared_text_input_edit_text_cursor_color">@color/primary_text_color</color>
  	<color name="shared_activity_toolbar_color">@color/toolbar_color</color>
  	<!--Styles.xml-->
  	<color name="shared_text_input_layout_text_color">@color/primary_text_color</color>
  	<color name="shared_input_interaction_edit_text_text_color">@color/primary_text_color</color>
  	<color name="shared_text_input_layout_background_color">@color/text_input_background_color</color>
  	<!--Admin Auth Activity-->
  	<color name="admin_auth_secondary_text_color">@color/description_text_color</color>
  	<color name="admin_auth_layout_background_color">@color/background_color</color>
  	<!--Add Profile Activity-->
  	<color name="add_profile_activity_label_text_color">@color/primary_text_color</color>
  	<color name="add_profile_activity_switch_text_color">@color/dark_text_color</color>
	```
4. **`colors_migrating.xml`**<br>
	This file contains color declarations which are supposed to be in color_defs.xml but has not been renamed yet to have actual color name instead of names linked to their use and components. This is a temporary measure to make sure other 4 color files follows the convention decided for them.
	This file should be deleted after all colors have been shifted to `color_defs.xml`.<br>