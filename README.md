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

* display_dialog
* choose_from_list
* choose_file
* choose_folder
* display_notification
* display_alert
* say_text

Each function requires an Applescript Record as its argument. Necessarily, the possible keys for this record are fixed by the library, but are consistent and will be explained in the documentation. Each function builds upon this general user-interaction framework:
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