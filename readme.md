# Hass MET Long Forecast Fork

This project is a fork of the [Home Assistant MET Component](https://github.com/home-assistant/core/tree/dev/homeassistant/components/met).

The goal is to test whether it is possible to extend the forecast from 5 days to 8 days.

I implemented changes in the `coordinator.py` file in the `fetch_data` method:

```python
// ...existing code...
self.daily_forecast = self._weather_data.get_forecast(time_zone, False, 0, 8)
self.hourly_forecast = self._weather_data.get_forecast(
    time_zone, True, 1, 24 * 7
)
// ...existing code...
```

Note: The original integration did not provide an end interval. As a result, the underlying [pyMetno](https://github.com/Danielhiversen/pyMetno/blob/master/metno/__init__.py) used default values of 25 hours and 6 days.

Once verified, I plan to create a PR to the official HASS integration to make this configurable.