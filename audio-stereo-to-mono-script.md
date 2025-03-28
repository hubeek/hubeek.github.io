# audio stereo to mono script

_Status: Published_
_Created: 2022-10-25 14:15:50_
_Tags: cli, terminal, audio, script_

## Convert all files as duo mono files
create a folder in which you want to convert the stereo clips to mono.
<code>
#!/bin/bash

for f in *.wav; do ffmpeg -i "$f" \
-filter_complex "[0:a]channelsplit=channel_layout=stereo[L][R]" \
-map "[L]" "${f%.*}_EXTRACTED_Lt.wav" \
-map "[R]" "${f%.*}_EXTRACTED_Rt.wav"; done
</code>