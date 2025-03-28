# heic convert

_Status: Published_
_Created: 2019-12-26 04:50:28_
_Tags: imagemagick, bash, terminal_

<code>
# convert any HEIC image in a directory to jpg format
magick mogrify -monitor -format jpg *.HEIC

# convert an HEIC image to a jpg image
magick convert example_image.HEIC example_image.jpg
</code>