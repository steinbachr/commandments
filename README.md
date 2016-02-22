# commandments
Shell Commands + Shortcuts I've found invaluable

Shell Commands
--------
**Find All Files Bigger Than N**<br />
`sudo find / -size +100M -ls `

Shell Functions
---------------
**Script allowing for the ability to `mark` and `unmark` directories**
```
SHELLMARKSDIR="$HOME/.shellmarks"
mkdir -p $SHELLMARKSDIR
function mark_alias { alias $(basename $1)="cd -P $1"; }

function mark { # Mark a directory
    symlink=$SHELLMARKSDIR/$1
    ln -ivhs "$(pwd)" $symlink && mark_alias $symlink
}
alias m=mark

function unmark { # Remove a mark
    symlink=$SHELLMARKSDIR/$1
    rm -iv $symlink
    if [ ! -f $symlink ]; then
        unalias $1
    fi
}
alias u=unmark

function shellmarks { # List all existing marks
    LINK_COLOR=$'\e[1;35m'
    RESET_COLOR=$'\e[0m'
    for symlink in $SHELLMARKSDIR/*; do
        echo "${LINK_COLOR}    $(basename $symlink) ${RESET_COLOR} -> $(readlink $symlink)"
    done
}

for symlink in $SHELLMARKSDIR/*; do # load all existing symlinks as aliases
    mark_alias $symlink
    test -e $symlink || rm $symlink # remove symlinks if source does not exist
done
```

Shell Workflows
-------
**Make USB Stick Bootable**
```
hdiutil convert -format UDRW -o ~/path/to/target.img ~/path/to/ubuntu.iso
diskutil list
diskutil unmountDisk /dev/diskN
sudo dd if=/path/to/downloaded.img of=/dev/rdiskN bs=1m
diskutil eject /dev/diskN
```

Python
-------
**Clear compiled .pyc files**<br />
`find . -name "*.pyc" -exec rm -rf {} \;`


Django
-------
**Show all Installed URL Routes**<br />
`/manage.py show_urls`


Android
--------
**Completely Wipe Android Studio (http://stackoverflow.com/questions/17625622/how-to-completely-uninstall-android-studio)**<br />
```
rm -Rf /Applications/Android\ Studio.app
rm -Rf ~/Library/Preferences/AndroidStudio*
rm ~/Library/Preferences/com.google.android.studio.plist
rm -Rf ~/Library/Application\ Support/AndroidStudio*
rm -Rf ~/Library/Logs/AndroidStudio*
rm -Rf ~/Library/Caches/AndroidStudio*
rm -Rf ~/AndroidStudioProjects
rm -Rf ~/.gradle
rm -Rf ~/.android
rm -Rf ~/Library/Android*
```


Packages
---------
`https://github.com/santinic/how2`
