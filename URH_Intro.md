# Universal Radio Hacker (URH)

## RTL-SDR RAW recording
  Raw recording makes no assumptions of data type or signal composition
1. Recording Settings:
  - Mode: RAW
  - Correct IQ: ON
  - Snap to grid: OFF
  - Filter bandwidth: Wide enough to cover the whole signal blob
  - Gain: Enough to clearly see bursts, not overload
2. Center the signal
  - playback signal to center and adjust bandwidth
3. Baseband Simple Recorder
  - configure
    - File Format: **WAV RF64**,WAV FULL, WAV SRICT
    - Sample Format: 8 bit PCM IQ, **16 bit PCM IQ**,32bit IEEE Float IQ
  - Select Save Folder
4. Sanity check
  - change Source to **Baseband File Player**
  - file manager maneuver to saved WAV file
  - press play to confirm saved file was recorded correctly
## What Universal Radio Hacker (URH)
Universal Radio Hacker is a tool for turning raw RF recordings into understandable digital messages
### Download and Install URH
  Go to the official project page:
  [Universal Radio Hacker GitHub](https://github.com/jopohl/urh)
  Follow [installation instructions](https://github.com/jopohl/urh#Installation) for latest release
  URH is open-source and widely used in RF/security research.
###
  
