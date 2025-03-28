# Fish, bash commands as functions 

_Status: Published_
_Created: 2016-12-20 02:28:23_
_Tags: terminal_

##edit start .bashrc
<code>
~/.config/fish/config.fish
</code>
##functions
<code>
p/crossword> function nrh
                               npm run hot
                       end
p/crossword> funcsave nrh
p/crossword> nrh
</code>
make Atom.app run from terminal:
<code>
ln -s /Applications/Atom.app/Contents/Resources/app/atom.sh /usr/local/bin/atom
</code>
make function in Fish:
<code>
nano ~/.config/fish/functions/atom.fish
</code>
some functions:
<code>
function atom
    bash -c 'atom .'
end
function pstorm
    bash -c 'open -a /Applications/PhpStorm.app .'
end
</code>

<code>
function xcodeclean
        command rm -rf ~/Library/Developer/Xcode/DerivedData/*
end
</code>

<code>
function ll
    ls -lahG $argv
end
</code>

<code>
function rmpoddata
    pod deintegrate
    rm -rf Pods
    rm -rf Podfile.lock
    pod install
end
</code>

<code>
function rmderiveddata
    sudo rm -rf ~/Library/Developer/Xcode/DerivedData/*
end

</code>