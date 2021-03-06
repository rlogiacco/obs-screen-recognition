# obs-screen-recognition

This script is designed to recognise specific content on your screen and change scenes within OBS based on that content.

### PLEASE NOTE: THIS SCRIPT IS NOT INTENDED TO BE RUN FROM INSIDE OBS AS AN "OBS SCRIPT". PLEASE FOLLOW THE USAGE INSTRUCTIONS CAREFULLY.

### ALSO NOTE: THIS ONLY WORKS WITH OFFICIAL OBS - NOT STREAMLABS OBS

## Hell Let Loose Map Detection

The initial use-case is to recognise when the map is open in Hell Let Loose, and change scenes in OBS so that map is not revealed to the live broadcast viewers.

The `hll` folder contains images which are always displayed when the HLL map is open, and a mask file to reduce the image down to where those images show. These images are organized for screen resolutions (currently only `1080p` and `1440p`). Use the "--show-debug-window" option to see what the script sees after applying the mask.

**With your contributions additional games and formats might be supported: submit your files via a Github Pull Request.**

## Usage
1. Clone/download repository and extract into any folder (e.g. Downloads)
2. Install Python 3.8. **Click "Add Python 3.8 to PATH at the bottom".**
3. Install a terminal app if you don't already have one e.g. [Git Bash](https://gitforwindows.org/)
4. Open up your terminal
5. Navigate to where you extracted this repository (e.g. `cd Downloads/obs-screen-recognition`)
4. Install the dependencies using pip in your terminal: `pip install -r requirements.txt`
5. Install the [obs-websocket plugin](https://obsproject.com/forum/resources/obs-websocket-remote-control-obs-studio-from-websockets.466/) for OBS (Windows Installer works fine)
6. Start (or restart) OBS (Note that Streamlabs OBS will not work)
7. Run the script providing the game screen format (either `1080p`, if you play in Full HD, or `1440p`, if you play in Quad HD) and the resources folder (only `hll` current provided) along with any other settings you want to override (use `--help` flag to get help on all the supported settings)
8. Since the script is not instantaneous (it takes a small amount of time to recognise the images, and a small amount of time to contact OBS), it is probably a good idea to look at the script's "Suggested OBS source delay" logs and set your scene delay (in OBS) to something around that. ~150ms seems to work well on the creator's hardware.

Default values are provided for each option, but if you find you often have to set the same options (like the screen format) you can customize the default value by updating the `defaults.json` file which allows to override every single option of the command line:

```json
{
    "monitor": 1,
    "format": "1080p",
    "scene_off": "Live Gaming",
    "scene_on": "Live Gaming (Map Covered)",
    "features": 500,
    "matches": 20,
    "port": 4444,
    "show_debug_window": true
}
```

Each option can also be provided via environment variables:

* `OBFUSCATOR_MONITOR`
* `OBFUSCATOR_FORMAT`
* `OBFUSCATOR_SCENE_ON`
* `OBFUSCATOR_SCENE_OFF`
* `OBFUSCATOR_FEATURES`
* `OBFUSCATOR_MATCHES`
* `OBFUSCATOR_PORT`
* `OBFUSCATOR_SHOW_DEBUG_WINDOW`


An executable shell script (`.bat`) can be created to start the script without having to get to the command line each and every time, like the `hll_obfuscator.bat` example file.