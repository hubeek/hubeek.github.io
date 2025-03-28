# masking cutting out shapes

_Status: Published_
_Created: 2014-08-02 17:18:41_
_Tags: Actionscript_

1) Inflexible hole cutting:

this.graphics.beginFill(0x666666);
this.graphics.drawRect(0,0,256, 256);
this.graphics.drawCircle(128,128,32);
this.graphics.endFill();
this will create a rectangle of 256 by 256 with a 64px hole in it.

2) Flexible hole cutting:

Obviously this will not work when you're not using the graphics class. In That case I would go with BlendMode.ERASE.

var spr:Sprite = new Sprite();
var msk:Sprite = new Sprite();

addChild(spr);
spr.addChild(msk)

spr.graphics.beginFill(0x666666);
spr.graphics.drawRect(0,0,256, 256);
spr.graphics.endFill();

msk.graphics.beginFill(0x000000);
msk.graphics.drawEllipse(0,0,64,64);
msk.graphics.endFill();
msk.x = 128;
msk.y = 128;

spr.blendMode = BlendMode.LAYER;
msk.blendMode = BlendMode.ERASE;