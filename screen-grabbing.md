# Screen grabbing

_Status: Published_
_Created: 2015-12-06 03:52:34_
_Tags: OF_

<code>
//Grab the screen image to file
if ( key == ' ' ) {
  ofImage image;  //Declare image object

  //Grab contents of the screen
  image.grabScreen( 0, 0, ofGetWidth(), ofGetHeight() );  

  image.saveImage( "screen.png" );  //Save image
}
</code>