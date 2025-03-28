# enum raw

_Status: Published_
_Created: 2015-04-23 03:49:38_
_Tags: swift_

<code>
enum GameStatus: Int {
  
  case initial = 0, playing, finished
}

var a = GameStatus.initial
a.rawValue // 0

var d = GameStatus(rawValue: 1)
d!.rawValue // 1
</code>