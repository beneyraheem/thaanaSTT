## Dhivehi subtitle generator

The process follows a few basic steps:
 * Extract audio from the video
 * Download STT pretrained model and setup inference pipeline
 * Run STT on the audio to transcribe the audio
 * generate a .srt file containing subtitles with timestamps

### Setup

* Clone the repo
* create  virtual env `py -m venv env`
* activate vertual env `.\env\Scripts\Activate`
* Install requirements `pip install -r requirements.txt`

 * you may need to setup FFmpeg locally

### Usage

The transcriber script requires an audio file as input.  
You can use the provided `audio_extract.py` to extract
audio from an input video file, and run further pre-processing
on the file. Ex: run it through RNNoise or Spleeter.

```shell
usage: audio_extract.py input output

positional arguments:
  input                 Input video file eg: video.mp4
  output                Output file name eg: audio.wav

```

Afterwards, run `dhivehi.py` with the following arguments

The script uses pyAudioAnalysis to segment audio into more 
manageable lengths by running a silence detection routine. For
better results, you might want to play around with the
`silence_window` and `silence_weight` options, until the 
segmented audio looks good.

Two sample audio files included inside /audio

```shell
usage: dhivehi.py input output

eg: dhivehi.py .\audio\1.mp3 1.srt

positional arguments:
  input                 Input audio file name
  output                Output file name

optional arguments:
  -h, --help            show this help message and exit
  --model_dir MODEL_DIR
                        STT model files directory
  --temp_dir TEMP_DIR   Temp files directory
  --silence_window SILENCE_WINDOW
                        Audio smoothing window
  --silence_weight SILENCE_WEIGHT
                        Audio silence probabilistic weight

```
