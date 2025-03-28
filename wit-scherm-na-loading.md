# wit scherm na loading

_Status: Published_
_Created: 2014-10-06 03:39:53_
_Tags: Actionscript_

na loader

<code>[Embed(source="../../../../../../bin/assets/menuscreen/bg.png")]</code>
<code>                                public var BM:Class;</code>
<code>                                public var backgroundBMP:Bitmap;</code>
                                
<code>                                public function MenuScreen()</code>
<code>                                {</code>
<code>                                                this.background = null;//forget this for the first screen// 'assets/menuscreen/bg.png';</code>
<code>                                                backgroundBMP = new BM();</code>
<code>                                                backgroundBMP.smoothing = true;</code>
<code>                                                addChild(backgroundBMP);</code>
<code>}</code>
                                                
