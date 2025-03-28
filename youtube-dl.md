# youtube dl

_Status: Published_
_Created: 2020-11-16 14:55:30_
_Tags: terminal_

## install youtube-dl
```
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```
## youtube-dl is replaced by yt-dlp
```
yt-dlp -x --audio-format mp3 --audio-quality 0 "$1" | awk '{gsub(/\[[^]]*\]/,""); print}'
alias yt='function _yt() { yt-dlp -x --audio-format mp3 --audio-quality 0 "$1" | awk "{gsub(/\\[[^\\]]*\\]/,\"\"); print}"; }; _yt'

```
## mp3
```
youtube-dl --extract-audio --audio-format mp3 URL-vid
```


## playlist
```
youtube-dl --extract-audio --audio-format mp3 -o "%(title)s.%(ext)s" URL-playlist
```
```
youtube-dl -cit --extract-audio --audio-format mp3 URL-playlist
```
