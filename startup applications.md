"startup applications" app in ubuntu shows the list of start up apps . there is a professional way to edit this list . if you are willing to be a professional .

in your home directory which is indicated by `~` symbol in documentations , there is a hidden folder named ".config" and has a child folder named "autostart" which has files with postfix "desktop" .

these files are list of config files for each program which should be run when a user logs in . inside of them are some config lines .

you can create , delete and edit these files . there is an attribute called `Hidden` and the value is boolean (true , false) .

```config
Hidden=false
```

if this attribute has value true . you can change it to false , if you wanna see its parent file in startup apps list .
