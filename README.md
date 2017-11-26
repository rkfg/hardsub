# Hardsub
A simple script to produce hardsubbed video suitable for Smart TVs. Anything other than plain SRT subtitles is not supported well
on hardware players so hardsub is preferred. Use -h to get a list of supported parameters.

# Notes
- The autodetected bitrate is the source bitrate plus 200 Kbit/sec. It's purely empirical.
- If the source video has FLAC audio I need to convert it to AAC because my TV plays it incorrectly shifting it to
1-2 seconds before video. You can disable this behavior with -a, then audio will always be copied as is.
- Use -i to get the stream numbers because indexes are zero-based but the script needs type-based numbers. An example: 0 - video, 1 - audio (eng), 2 - audio (fre), 3 - audio (ger), 4 - subs (eng), 5 - subs (fre), 6 - subs (ger). Here, the indexes are consecutive but we need them to be relative to the first index of their type. Namely: 0 - audio (eng), 1 - audio (fre), 2 - audio (ger), 0 - subs (eng), 1 - subs (fre), 2 - subs (ger). The analyzing function does this math for you.
- video stream selection is not supported at the moment as it's very rare to have more than one video stream in a file (personally, I've never seen that). Still, it's pretty easy to add if needed.
- text and picture-based subtitles are supported, currently the picture-based overlay approach is chosen if the subtitle type contains "pgs" which is common for BluRay streams. There could be more such formats that I'm unaware of.
- Softsubs are always discarded as that's the whole point of the script.
- HEVC/H.265 is encoded in the source pixel format, I noticed that my TV supports 10-bit H.265 though it doesn't support
10-bit H.264 so no need to make the quality worse without the real need. YMMV. For H.264 the script forces y420p.
