# list finale files in dir to txt file

_Status: Published_
_Created: 2019-06-21 03:48:25_
_Tags: terminal_

<code>
ls -1 | sed -e 's/ C.musx$//' > songs.txt
</code>