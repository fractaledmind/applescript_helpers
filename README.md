# AppleScript User-Interaction Helper Functions

This is an AppleScript library for the primary user-interaction functions available to AppleScript. This library provides a terse means by which to access these user-interaction functions:

* display dialog
* choose from list
* choose file
* choose folder
* display notification
* display alert
* say

In each case, this library provides a consistent syntax for utilizing the full range of optional parameters for each function, while also ensuring that each user-interaction is always presented front-and-center and will fail silently. 

At its heart, this library contains these functions (which map to those above):

* display_dialog(record)
* choose_from_list(record)
* choose_file(record)
* choose_folder(record)
* display_notification(record)
* display_alert(record)
* say_text(record)

## Features/Advantages
Each function builds upon this general user-interaction framework:
<pre><code>
try
	tell application (path to frontmost application as text)
		display dialog "Hello world!"
	end tell
on error errText number errNum
	if not (errNum is equal to -128) then
		tell application id "sevs"
			display dialog "Hello world!"
		end tell
	end if
end try
</code></pre>

While verbose, this skeleton will ensure that user-interactions are always front-and-center and fail gracefully. This library allows you to present all user-interactions this way without the hassle of the skeleton. 

Each function also requires an Applescript Record as its argument. Necessarily, the possible keys for this record are fixed by the library, but are consistent and will be explained in the documentation. The advantage of this approach is simply concision and consistency. The library functions take care of the syntax