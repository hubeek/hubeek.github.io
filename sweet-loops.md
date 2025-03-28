# Sweet Loops

_Status: Published_
_Created: 2016-01-25 11:58:58_
_Tags: swift_

<code>
for section in sections {
    var foundTheMagicalRow = false
    for row in rows {
        if row.isMagical {
            foundTheMagicalRow = true
            break
        }
    }
    if foundTheMagicalRow {
        //We found the magical row! 
        //No need to continue looping through our sections now.
        break
    }
}
</code>
is the same as:
<code>
sectionLoop: for section in sections {
    rowLoop: for row in rows {
        if row.isMagical {
            break sectionLoop
        }
    }
}
</code>
from:
http://krakendev.io/
