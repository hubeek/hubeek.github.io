# Icon create

_Status: Published_
_Created: 2016-07-31 16:06:44_
_Tags: swift, terminal, bash_

after: brew install imagemagick<br />
create iconcreate.sh<br />
<code>
#!/bin/bash
for size in {76,40,29,60,57,50,72,167}; do for scale in {1,2,3}; do
    if [[ $scale == 1 ]]; then
        filename="icon_${size}.png"
    else
        filename="icon_${size}@${scale}x.png"
    fi
    gm convert "icon.png" -resize "$(( $scale * $size ))x$(( $scale * $size ))" $
done; done
</code>

or
sh iconcreate.sh icon.png
<code>
convert $1 -resize 16x16      Icon-16.png
convert $1 -resize 32x32      Icon-16@2x.png
convert $1 -resize 29x29      Icon-Small-29.png          # Settings on iPad and iPhone, and Spotlight on iPhone
convert $1 -resize 58x58      Icon-Small-29@2x.png
convert $1 -resize 87x87      Icon-Small-29@3x.png
convert $1 -resize 32x32      Icon-32.png
convert $1 -resize 64x64      Icon-32@2x.png
convert $1 -resize 40x40      Icon-Small-40.png       # Spotlight
convert $1 -resize 80x80      Icon-Small-40@2x.png       # Spotlight
convert $1 -resize 120x120    Icon-Small-40@3x.png       # Spotlight
convert $1 -resize 50x50      Icon-Small-50.png       # Spotlight on iPad 1/2
convert $1 -resize 57x57      Icon-57.png                # Home screen on non-Retina iPhone/iPod
convert $1 -resize 114x114    Icon-57@2x.png             # Home screen for Retina display iPhone/iPod
convert $1 -resize 120x120    Icon-60@2x.png          # Home screen on iPhone/iPod Touch with retina display
convert $1 -resize 180x180    Icon-60@3x.png          # Home screen on iPhone 6 Plus
convert $1 -resize 72x72      Icon-72.png             # App Store and Home screen on iPad
convert $1 -resize 144x144    Icon-72@2x.png          # Home screen for "The New iPad"
convert $1 -resize 76x76      Icon-76.png             # Home screen on iPad
convert $1 -resize 152x152    Icon-76@2x.png          # Home screen on iPad with retina display
convert $1 -resize 228x228    Icon-76@3x.png
convert $1 -resize 83.5x83.5  Icon-83,5.png
convert $1 -resize 167x167    Icon-83,5@2x.png
convert $1 -resize 128x128    Icon-128.png
convert $1 -resize 256x256    Icon-128@2x.png
convert $1 -resize 256x256    Icon-256.png
convert $1 -resize 512x512    Icon-256@2x.png
convert $1 -resize 512x512    Icon-512.png
convert $1 -resize 1024x1024  iTunesArtwork@2x.png   # App list in iTunes for devices with retina display
convert $1 -resize 1024x1024  Icon-512@2x.png
convert $1 -resize 512x512    iTunesArtwork.png       # Ad Hoc iTunes
</code>