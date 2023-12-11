FFmpeg README
=============

FFmpeg is a collection of libraries and tools to process multimedia content
such as audio, video, subtitles and related metadata.

`[NOTE] SOLUTION for v4l2_m2m_enc issues`

When using ffmpeg -i ... -c:v h264_v4l2m2m ... , there are many warnings and some unexpected exits (on raspberry pi). `COMMIT 129fb83` will make you avoid them.

- warning (frequent), "Non-monotonous DTS in output stream"

- warning (sparse), "All capture buffers returned to userspace"

`Because` formatters treat a header and a key-frame as 2 separate frames with MPEG_VIDEO(HEADER_MODE_SEPARATE). So, "joined header mode" is preferable.


- error, "Could not find codec parameters for stream 0"

- error, "non-existing PPS 0 referenced"

`Because` extradata (e.g. SPS/PPS) is not created at init. Encoding dummy frame at init avoids this issue. But there need more cleanups with flushing buffer and timing (Experts about v4l2 buffers are needed for help)



## Libraries

* `libavcodec` provides implementation of a wider range of codecs.
* `libavformat` implements streaming protocols, container formats and basic I/O access.
* `libavutil` includes hashers, decompressors and miscellaneous utility functions.
* `libavfilter` provides means to alter decoded audio and video through a directed graph of connected filters.
* `libavdevice` provides an abstraction to access capture and playback devices.
* `libswresample` implements audio mixing and resampling routines.
* `libswscale` implements color conversion and scaling routines.

## Tools

* [ffmpeg](https://ffmpeg.org/ffmpeg.html) is a command line toolbox to
  manipulate, convert and stream multimedia content.
* [ffplay](https://ffmpeg.org/ffplay.html) is a minimalistic multimedia player.
* [ffprobe](https://ffmpeg.org/ffprobe.html) is a simple analysis tool to inspect
  multimedia content.
* Additional small tools such as `aviocat`, `ismindex` and `qt-faststart`.

## Documentation

The offline documentation is available in the **doc/** directory.

The online documentation is available in the main [website](https://ffmpeg.org)
and in the [wiki](https://trac.ffmpeg.org).

### Examples

Coding examples are available in the **doc/examples** directory.

## License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under
GPL. Please refer to the LICENSE file for detailed information.

## Contributing

Patches should be submitted to the ffmpeg-devel mailing list using
`git format-patch` or `git send-email`. Github pull requests should be
avoided because they are not part of our review process and will be ignored.
