# Hardsub
A simple script to produce hardsubbed video suitable for Smart TVs. ASS-styled subtitles are not supported well so hardsub
is preferred. Use -h to get a list of supported parameters.

# Notes
- The autodetected bitrate is the source bitrate rounded down to hundreds plus 200. It's purely empirical.
- If the source video has FLAC audio I need to convert it to AAC because my TV plays it incorrectly shifting it to
1-2 seconds before video. You can disable this behavior with -a, then audio will always be copied as is.
- Subtitle tracks start with 0 though ffprobe usually reports them starting with #0:2, subtract the offset manually.
By default the 0th track is used.
- Softsubs are always discarded as that's the whole point of the script.
- nvenc NVIDIA's hardware encoding is always used (5x acceleration or better usually). No autodetection
or force software encoding options currently.
- HEVC/H.265 is encoded in the source pixel format, I noticed that my TV supports 10-bit H.265 though it doesn't support
10-bit H.264 so no need to make the quality worse without the real need. YMMV. For H.264 the script forces y420p.
