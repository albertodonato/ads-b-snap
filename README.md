# Snap package for ADS-B, Mode S, and Mode 3A/3C demodulator and decoder

[![Snap Package](https://snapcraft.io/ads-b/badge.svg)](https://snapcraft.io/ads-b)

This snap provides the `dump1090` ADS-B, Mode S, and Mode 3A/3C demodulator and
decoder to receive and decode aircraft transponder messages received via an SDR
(software defined radio) USB dongle.

It uses the [dump1090-fa](https://github.com/flightaware/dump1090) fork from
FlightAware.

It also includes the [tar1090](https://github.com/wiedehopf/tar1090) web
interface to display received aircrafts information and positions on map.

The web interface is available by default on port `8080` (see below for config
options).

Furthermore, information for received ADB-S messages can be displayed on the
console with the `adb-s.view` too.

The snap can be installed from the store via:

```bash
    sudo snap install ads-b
```

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/ads-b)


## Enabling services

Services provided by the snap are disabled by default. After connecting
interfaces and the the SDR USB device, they can be started with

```bash
    sudo snap start --enable ads-b
```


## Feeding data to Flightradar24

It's possible to feed collected data to
[Flightradar24](https://www.flightradar24.com/). This requires specifying the
sharing key (which can be obtained from the account page).

To enable sharing run

```bash
    sudo snap set ads-b fr24.key=<KEY>
    sudo snap start --enable ads-b.fr24feed
```


## Snap configuration options

The snap has a few configuration options:

* `coord.lat`, `coord.lon`: GPS coordinates of the receiver
* `fr24.key`: account key for the Flightradar24 feeder
* `web.port`: TCP port for the web interface (default: `8080`)

Services are automatically restarted on configuration changes.
