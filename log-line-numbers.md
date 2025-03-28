# Log Line Numbers

_Status: Published_
_Created: 2014-09-23 09:52:00_
_Tags: Actionscript_

trace(">",new Error().getStackTrace().match(/(?<=:)[0-9]*(?=])/g)[0]);