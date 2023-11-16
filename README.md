# 4d-tips-applescript-launcher
Applet that catches and redirect 4DD double click events

```applescript
on open theFiles
	if (count of theFiles) is not 0 then
		set theFile to item 1 of theFiles
		set thePath to quoted form of POSIX path of theFile
		do shell script "open -a 4D " & thePath
	end if
end open
```

see `man open` for `open` arugments. by default, the path is simply used open 4D.

* edit the `do shell script` line to meet local needs.
* `LSBackgroundOnly` and `LSUIElement` are noth set to `YES`.

## Background

When the user double clicks a file associated with a 4D built application, the [`application:openFile:`](https://developer.apple.com/documentation/appkit/nsapplicationdelegate/1428612-application?language=objc) delegate method is invoked although the app does not process it, rather, it always opens the embedded structure/project and the last opened data file. the end user thinks the double clicked data file is chosen but that is not how 4D selected its data file.

This workaround is expected to do the following:

* register itself has owner and editor of the 4DD and DATA file extensions. see info.plist. you might have to launch it once.
* on launch, take the first file path from arguments and open 4D (or whatever app specified in the script)
* terminate
