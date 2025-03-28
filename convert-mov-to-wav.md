# Convert mov to wav

_Status: Published_
_Created: 2025-03-28 02:54:21_

```bash
#!/bin/bash

shopt -s nocaseglob nullglob  # Enable case-insensitive matching and skip loop if no match

for file in *.mov; do
  echo "Converting: $file"
  ffmpeg -i "$file" -vn -acodec pcm_s16le "${file%.*}.wav"
done
```