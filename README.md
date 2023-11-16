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
