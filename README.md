# Bresser WiFi Weather Station for Home Assistant OS

## *Important: My weather station at home is no longer working, I can no longer test, fix or support anything in this repository*

## If you are using another Home Assistant installation method, check the sibling repository [bresser-home-assistant](https://github.com/raphv/bresser-home-assistant)

A Home Assistant OS Addon to retrieve data from a Bresser Personal Weather Station.

The [Bresser WiFi ClearView Weather Station](https://www.bresser.de/en/Weather-Time/BRESSER-WIFI-ClearView-Weather-Station-with-7-in-1-Sensor.html) comprises an external sensor and an indoor base station.
These communicate via a 868 MHz frequency, but the indoor base station also  has WiFi capability.
One benefit of communicating through the indoor station rather than decoding the RF transmission is to access data from sensors that are on the base station itself.
Its capabilities include upload to Weather Underground, but also to any arbitrary Web server, including a local one.
The weather station doesn't expose any open ports so the only way to access data is to create a web server and to listen to requests.

I have created a Python script that listens to requests on `/weatherstation/updateweatherstation.php`, stores this data in a dictionary, then serves it on another URL (`/data`) that Home Assistant can access as sensors via the [REST integration](https://www.home-assistant.io/integrations/sensor.rest/).
The Python script also logs weather data as one CSV file per day.

## How to use?

### Step 1: Install the Add-on

[![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fraphv%2Fbresser-pws-haos-addon)

### Step 2: Update your Home Assistant configuration

You need an addon that lets you edit files on your Home Assistant instance (e.g. SSH, SMB, Editor).
* Add the pws-sensors.yaml file
* Edit your configuration.yaml file, e.g. with the following line:
`rest: !include pws-sensors.yaml`
