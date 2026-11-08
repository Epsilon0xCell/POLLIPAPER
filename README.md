![Intro: a painter's hand brushing wet storm grey paint over the fair blue sky of a wall mural beside a rain streaked window, the gilt frame of the finished mural section at the right](intro-banner.png)


# POLLIPAPER

<p align="center"><img src="logo.png" alt="POLLIPAPER logo: an ornate gilt frame hung on cracked cream plaster, inside it a patch of wall painted with a perfect blue sky and one white cloud, the paint's rough edge showing where the mural meets bare plaster" width="200"></p>

![Banner: a huge gilt framed mural of green fields under a fair blue sky painted across a cream plaster wall, while the real window at the left shows grey rain outside](banner.png)

![Scene](scene.svg)

POLLIPAPER is a Windows desktop wallpaper application written in Python
with tkinter. It generates images with the Pollinations AI image service,
saves them locally, and sets them as the Windows desktop wallpaper through
the Windows `IDesktopWallpaper` COM API. It can also build prompts from
local weather data and draw a weather information overlay onto the image.


![Separator](sep-heavy.svg)

## Platform

Windows only. The code imports `winreg` and `pythoncom`, uses
`ctypes.HRESULT`, and sets the wallpaper through a Windows COM interface,
so it does not run on macOS or Linux.


![Separator](sep-heavy.svg)

## Features

- Generate wallpapers from a custom text prompt (the prompt is
  percent-encoded into the Pollinations request URL)
- Automatic wallpaper changing on an interval, minimum 5 minutes
- Wallpaper styles: center, tile, stretch, fit, fill (1920x1080) and span
  (3840x1080)
- Enhance option, passed to the Pollinations API, with the returned
  enhanced prompt read back from the image EXIF metadata when present
- Model selection (default `flux`)
- Weather-based prompts and an optional weather overlay, using
  OpenWeatherMap
- Overlay opacity (0 to 255), position, background color, and an optional
  drop shadow
- Temperature display in Fahrenheit or Celsius (weather data is fetched
  in metric units and converted for display when Fahrenheit is selected)
- Prompt history, most recent 20 prompts, saved to `prompt_history.json`
- Settings saved to `background_settings.json` and reloaded on start
- Generated images are kept in the `POLLINATIONS_BACKGROUNDS` folder; the
  5 most recent backgrounds and the most recent overlaid wallpaper are
  kept, older ones are deleted

> **Mural note:** the change interval has a floor of five minutes. Shorter intervals cannot be set in the Options menu.


![Separator](sep-heavy.svg)

## Requirements

- Windows, with Python 3
- The packages in `requirements.txt`: requests, Pillow, comtypes, and
  pywin32
- tkinter, which ships with the standard Windows Python installer
- An OpenWeatherMap API key, only for the weather features


![Separator](sep-heavy.svg)

## Installation

```bash
git clone https://github.com/Epsilon0xCell/POLLIPAPER.git
cd POLLIPAPER
pip install -r requirements.txt
```


![Separator](sep-heavy.svg)

## Usage

```bash
python POLLIPAPER.py
```

1. Enter a prompt in the text box, or pick one from the history dropdown.
2. Click Start to generate and set wallpapers, and Start again (it becomes
   Stop) to stop.
3. Use the Options menu to set the interval (in minutes, minimum 5) and
   your OpenWeatherMap API key, and to pick the temperature unit.
4. To use weather-based prompts or the weather overlay, set an
   OpenWeatherMap API key first (Options menu, or the
   `OPENWEATHER_API_KEY` environment variable). If a weather request
   fails, the app reports it and continues without weather data instead
   of crashing.


![Separator](sep-heavy.svg)

## Limitations

- The weather location is not configurable in the UI. The code defaults
  to Rochester, US; change the default arguments of `fetch_weather_data`
  in `POLLIPAPER.py` to use a different city.
- Weather requests time out after 15 seconds and are not retried inside
  the weather fetcher itself; image generation is retried up to 5 times
  with backoff.
- Settings and history files are stored in the folder the app is started
  from, and a corrupt settings or history file is ignored (defaults or
  an empty history are used) rather than preventing startup.


![Separator](sep-heavy.svg)

## License

MIT, see the [LICENSE](LICENSE) file.


![Separator](sep-heavy.svg)

## Acknowledgments

- [Pollinations AI](https://pollinations.ai/) for the image generation service
- [OpenWeatherMap](https://openweathermap.org/) for weather data
