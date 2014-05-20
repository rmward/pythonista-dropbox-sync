# pythonista-dropbox-sync

A Pythonista script and supporting module to sync [Pythonista](http://omz-software.com/pythonista/) files with [Dropbox](http://dropbox.com), based on and [original script](https://gist.github.com/mlgill/8311088) and [module](https://gist.github.com/mlgill/8311046) by Michelle Gill, but with my own improvements. 

## Motivation

Pythonista does not include any sync or backup functionality. This script makes a little hacky progress toward adding that functionality. 

In particular, I view this script as a first step in linking my scripts in Pythonista to projects in GitHub. In fact, it's how this script was developed. 

## Installation and use

Go to [Dropbox's developer page](https://www.dropbox.com/developers/apps/create) to register a new app. Be sure to: 

- Make it a "Dropbox API app".
- Tell Dropbox that your app needs access to "Files and datastores". 
- Tell Dropbox that the app can be limited to its own folder. 
- Give it a unique name (for example, "Pythonista Sync YOURINITIALS"). 
- Note your app key. 
- Note your app secret. 

Otherwise, default setting should be fine. 

Make sure DropboxSync.py and dropboxsetup.py are stored in the same directory, and that it's the directory in Pythonista you want to sync—currently you'll probably want this to be Pythonista's root directory. Then open DropboxSync.py and run it.

On first run, DropboxSync will request that you enter a name for the dropbox token file (I recommend that it start with "." so that it's hidden on many systems). It will then request that you enter your app key and app secret. The app then reads the current Pythonista directory and subdirectories, the target Dropbox directory, and ensures that the latest version of each file (based on time stamp) is stored in both locations. 

This input is stored so it isn't needed subsequently. The script just reads the stored data and performs the sync without requiring interaction. 

One note on usage: currently I have individual Dropbox files in the DropboxSync app folder hard-linked to their counterparts in my local git repo. This way changes made in Pythonista will propagate to the copies in the repo, and vice versa. Given my lack of knowledge of how Dropbox treats hard links, this seems iffy, but it works OK so far with one caveat—updating a file in the repo doesn't cause Dropbox to rescan its counterpart in the app folder. There are a vareity of ways to trigger a manual rescan, but I'd like to have it work automatically. As it is, this still makes integrating Pythonista with GitHub much easier. 

## Improvements over original script

- The original "dropboxsetup" module created a directory by default to store the Dropbox token. I've removed all support for this. 
- The original "DropboxSync" script required that multiple things be hardcoded into the script: the app key, app secret, and Dropbox token file name. Not only is this not very user friendly, but it means that I couldn't directly put a working version of this script on GitHub. The script now requests these items interactively. 
- Added support to store these inputs in the "pickled" state file. 

## Future improvements

- Currently, for this script to backup all of your Pythonista files, it must reside in the Pythonista root directory. If it's possible, I'd like to be able to store it in its own subdirectory. 
- I'd like to reintroduce the option to use a subdirectory to store the Python session file in a way that makes it optional. 
- The script relies on modification date/times to decide which version of a file is newer. I need to do some debugging to determine whether these times are universal or time zone dpendent—I wouldn't want a change in timezone on a device to cause the wrong file to be kept. 
- I'd like to have both a "sync" mode and an "archive" mode. 
- I need to clean up the code and comments to change it to my "house style"; currently it still looks very much like Michelle's original script. 


## License

See included license file. In addition to crediting me, you should probably also credit Michelle, the original author. Though she didn't specifically provide a license for the code, she provided a very nice base for this and deserves credit. . 
