# Bresser WiFi Weather Station for Home Assistant

The [Bresser WiFi ClearView Weather Station](https://www.bresser.de/en/Weather-Time/BRESSER-WIFI-ClearView-Weather-Station-with-7-in-1-Sensor.html) comprises an external sensor and an indoor base station.
These communicate via a 868 MHz frequency, but the indoor base station also  has WiFi capability.
One benefit of communicating through the indoor station rather than decoding the RF transmission is to access data from sensors that are on the base station itself.
Its capabilities include upload to Weather Underground, but also to any arbitrary Web server, including a local one.
The weather station doesn't expose any open ports so the only way to access data is to create a web server and to listen to requests.

I have created a Python script that listens to requests on `/weatherstation/updateweatherstation.php`, stores this data in a dictionary, then serves it on another URL (`/data`) that Home Assistant can access as sensors via the [REST integration](https://www.home-assistant.io/integrations/sensor.rest/).
The Python script also logs weather data as one CSV file per day.
