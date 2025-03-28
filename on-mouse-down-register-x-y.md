# on mouse down register x y

_Status: Published_
_Created: 2014-05-31 17:28:42_
_Tags: javascript_

var clicking = false;

$('.selector').mousedown(function(){
    clicking = true;
    $('.clickstatus').text('mousedown');
});

$(document).mouseup(function(){
    clicking = false;
    $('.clickstatus').text('mouseup');
    $('.movestatus').text('click released, no more move event');
})

$('.selector').mousemove(function(){
    if(clicking == false) return;

    // Mouse click + moving logic here
    $('.movestatus').text('mouse moving');
});