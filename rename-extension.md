# rename extension

_Status: Published_
_Created: 2016-07-31 14:55:29_
_Tags: terminal_

<code>
for file in *.html
do
 mv "$file" "${file%.html}.txt"
done
</code>