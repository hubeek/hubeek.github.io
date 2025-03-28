# string replace

_Status: Published_
_Created: 2014-12-02 04:36:00_
_Tags: Actionscript_

var str:String = "AS3 rocks!";
var search:String = "AS3";
var replace:String = "Actionscript 3";

function strReplace(str:String, search:String, replace:String):String {
 return str.split(search).join(replace);
}

trace(strReplace(str, search, replace)); //Outputs Actionscript 3 rocks!