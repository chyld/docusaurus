---
sidebar_position: 6
---

# Scratch Pad

## tmux

- clipboard is integrated with the system
- to copy (press p-[, space to start selection, press enter to copy)
- to paste (press p-])
- you can also use VI search features to find what you are looking for

## scripts

```bash
- `rsync -avz (source) (destination)`
- list all the files in a directory (including subdirectories) and sort by datetime
- `find . -type f -exec ls -l --time-style=long-iso {} + | sort -k 6,7`
- convert webm to mp4 using x264 video and aac audio codecs
- `ffmpeg -i input.webm -c:v libx264 -c:a aac output.mp4`
- `convert hello.png goodbye.jpg` # image format conversion
```
