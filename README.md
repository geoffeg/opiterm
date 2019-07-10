Opiterm is a simple way to integrate 1password with iTerm2.

Opiterm is similar to tools such as sudolikeaboss and tmux-1password. When you need to enter a password in iTerm2, a hotkey opens a small window running op + fzf, lets you choose your password and the selected password is sent to the parent window.

Requirements:
* [op](https://support.1password.com/command-line/)
* [fzf](https://github.com/junegunn/fzf)
* [jq](https://stedolan.github.io/jq/)

Components:
* opfzf: op + fzf. Uses fzf to help you find and choose your password. Basically a fork of Yarden Sod-Moriah's "tmux-1password" main.sh script.
* opiterm-trigger: The iterm "coprocess" script used to create a new terminal window and execute the "opiterm" script
* opiterm: Launches opfzf, grabs the password and sends it to the iTerm window that was focused when the hotkey was pressed:

Setup:
1. Put opfzf and opterm somewhere in your path. (I have a "bin" directory in my $HOME.) Regardless of where you put the scripts, make sure it is in your bash path and the scripts are executable (chmod a+x opfzf opiterm).
2. Put opiterm-trigger somewhere. This doesn't need to be in your path since it's only called by iTerm. I put it in ~/Library/Application Support/iTerm2/Scripts/. 
3. Load the provided opiterm-iterm.profile into iTerm2 to create a small window dedicated to opiterm. Be sure to call this profile "opiterm".
4. Setup op if you haven't done that already.
5. In your main iTerm profile, create a hotkey to launch opiterm-trigger:
    1. Preferences -> Profiles -> Keys -> "+" to create a new key mapping
	  2. Choose a key map of your choosing.
	  3. Select "Run Coprocess"
	  4. Provide the path to wherever you stored opiterm-trigger in #2 above.

Usage:
* At a password prompt, hit the hotkey you setup above, a small window will launch. If this is the first time you've launched op today, you'll be prompted for your master password. opfzf will launch, letting you choose your password. Press enter when you've selected the correct password and the password will be sent to the opening iTerm window.

Caveats:
* Only a small subset of 1Password item types will work. Right now, just logins.

Todo:
* Switch to the Python API to allow:
    * Creating the opfzf window where the cursor was (this might be possible with apple script)
