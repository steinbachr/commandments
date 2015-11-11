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

Python
-------
**Clear compiled .pyc files**<br />
`find . -name "*.pyc" -exec rm -rf {} \;`


Django
-------
**Show all Installed URL Routes**<br />
`/manage.py show_urls`
