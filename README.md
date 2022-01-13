# aiortc-hwaccel

AIORTC uses the PyAV bindings for H264 decoding. We build the `hwaccel` branch (gpu accelerators) of this library from source:

```
git clone git@github.com:PyAV-Org/PyAV
cd PyAV
git checkout hwaccel
# Installs all dependecies including ffmpeg
source scripts/activate.sh 
./scripts/build-deps
make
```

In your aiortc project you need to replace the `h264` with `h264_cuvid` when specifying the codec: https://github.com/aiortc/aiortc/blob/01ff209cc38e887edeb05cba1845cf458b31a0ac/src/aiortc/codecs/h264.py#L106

In the sample h264 `parser.py` code, it runs h264 decoder on a sample ffmpeg video on both cpu (`h264`) and gpu(`h264_cuvid`).

## Troubleshoot
If you faced `configure: error: libx264 not found` then the following solves the issue:
```
sudo apt-get install yasm libvpx libx264
```
