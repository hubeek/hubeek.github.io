# Same Random Seed

_Status: Published_
_Created: 2016-09-16 03:00:20_
_Tags: swift_

<code>
var r = srand48(1)  //()
var r1 = drand48()  //0.04163034477187821
var r2 = drand48()  //0.4544924447286292
var r3 = drand48()  //0.8348172181669149


var s = srand48(1)
var s1 = drand48()  //0.04163034477187821
var s2 = drand48()  //0.4544924447286292
var s3 = drand48()  //0.8348172181669149

</code>