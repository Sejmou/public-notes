This solution relies on Enjoyable, an open source tool

use e.g. for games w/o native gamepad support
see also [YouTube video](https://www.youtube.com/watch?v=bylk5VRlJPE) and [Reddit post](https://www.reddit.com/r/medicalschoolanki/comments/jtlc46/gamepad_mapping_on_macos_big_sur/)
## Setup Enjoyable
### Pt 1. Download/Install
1. download latest Enjoyable release from [GitHub Releases page](https://github.com/shirosaki/enjoyable/releases) (v1.2.1 at the time of this writing; yes, it's from 2015  lol - could probably use website link as well, but this seems more trustworthy to me)
2. unzip
3. Move `.app` file to your Applications folder
4. as this is an unsigned app, you will have to right click the app in the Applications folder while holding the Cmd key for the 'Open' option to even show up (if this is your first time adding apps from outside the app store you might have to [enable installation of apps from outside the App Store](https://www.macworld.com/article/672947/how-to-open-a-mac-app-from-an-unidentified-developer.html#:~:text=Security%20Tips.-,How%20to%20open%20apps%20not%20from%20Mac%20App%20Store,-By%20default%20macOS) as well)

### Pt. 2: Give necessary permissions
1. go to Mac's System Preferences.
2. go to Privacy & Security.
3. click the lock to make changes and input your password.
4. scroll down to "Accessibility".
5. under “Accessibility”, uncheck then check “Enjoyable” (add app via + sign if not present)
6. scroll down to "Input Monitoring"
7. under “Input Monitoring”, uncheck then check “Enjoyable” (justl like for "Accessibility").

## Configure keybindings
Once the app starts
0. (Optional, but recommended) create a new profile
1. hit any button on your controller that you wish to remap => the UI will jump to the correct button no./axis automatically
2. choose whatever you want to happen on press of the associated button (pick from the existing options)
	- for "Press a key", you will have to click into the empty field, then hit the key. This will set a key binding
3. Repeat steps and 1 and 2 for every keybinding you want to set up
4. (Important) Make sure to enable Enjoyable! Either
	- Right click on the icon in Dock -> Enable
	- Pick option from the Menu Bar (Mappings -> Enable) while Enjoyable is focused
	- Hit Cmd + R while Enjoyable is focussed

## Import/Export existing keybindings
Find the options in the menu bar, should be self-explanatory. Enjoyable uses a custom `.enjoyable` extension for the config files