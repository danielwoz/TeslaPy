# TeslaPy

A Python implementation of the client side interface to the Tesla Motors API based on [unofficial documentation](https://tesla-api.timdorr.com/). The REST API provides functionality to monitor and control the vehicle remotely.

## Overview

*teslapy.py* depends on Python [requests](https://pypi.org/project/requests/). The `Tesla` class extends `requests.Session` and inherits methods like get and post that can be used to perform API calls. It implements custom OAuth 2.0 Password Grant, since *email* instead of *username* is used by the Tesla Motors API to authenticate users. The authentication token is cached to disk for reuse and is refreshed automatically when needed. The class provides a convenience method `api` to use named endpoints listed in *endpoints.json*, instead of using inherited get and post methods. The `Vehicle` class extends `dict` and is used to store vehicle data returned by the API. It also implements a method to wake up the vehicle and a method to list known option codes.

Basic usage of the module:

```python
import teslapy
with teslapy.Tesla(EMAIL, PASSWORD, CLIENT_ID, CLIENT_SECRET) as tesla:
	tesla.fetch_token()
	vehicles = tesla.vehicle_list()
	vehicles[0].api('HONK_HORN')
```

An advanced usage example that shows more features of the module is *menu.py*. It requires credentials to authenticate with the Tesla Motors API and it depends on [geopy](https://pypi.org/project/geopy/) to convert GPS coordinates to a human readable address:

![](media/menu.png)

*gui.py* is a graphical interface version of the advanced usage example using `tkinter`:

![](media/gui.png)

## Installation

Install [requests](https://pypi.org/project/requests/) and [geopy](https://pypi.org/project/geopy/) using [PIP](https://pypi.org/project/pip/):

`pip install requests geopy`

or on Ubuntu as follows:

`sudo apt-get install python-requests python-geopy`

Put *teslapy.py*, *menu.py*, *gui.py*, *endpoints.json* and *option_codes.json* in a directory and run *menu.py* or *gui.py*.

Python 2.7+ and 3.4+ are supported.