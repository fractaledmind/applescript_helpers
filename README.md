# AppleScript Helper Functions

These are two sets of Applescript functions that make common tasks easier, cleaner, and simpler. One set is aimed specifically at building [Alfred workflows](http://www.alfredforum.com/forum/3-share-your-workflows/), while the other is more generally usefully for generating Applescript's own user-interaction dialogs.


## User-Interaction

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

## Alfred Functions

This Applescript grants quick access to certain common functions in building and running Alfred workflows. Many of the functions are from [qlassiqa's qWorkflow library](https://github.com/qlassiqa/qWorkflow). Functions include:

* get_path() = returns POSIX path to `cwd`
* get_bundle() = returns workflow's `bundleid`
* init_paths() = ensures workflow's `storage` and `cache` paths exist
* get_cache() = returns POSIX path to workflow's `cache` directory
* get_storage() = returns POSIX path to workflow's `storage` directory
* get_home() = returns POSIX path to user's `home` directory
* mdfind(query) = returns list of results from `mdfind`

In addition to this functions, most of which are derived from [qlassiqa's qWorkflow library](https://github.com/qlassiqa/qWorkflow), I have also included a function to read simple JSON (i.e. no nesting). This proves helpful for `settings` or `preferences` files created in workflows. Simply pass the JSON string to the `read_json(json)` function. It returns an Applescript record, the keys of which will all be prepending with `_`. For example, the JSON:
```
{
    "type": "user",
    "user_id": "12345678",
    "api_key": "xxxxxxxxxxxxxxxxxxxxx"
}
``` 
will return the Applescript record: `{_type:"user", _user_id:"12345678", _api_key:"rf8L5AZdrVlK9NMTXDVuotok"}`.

