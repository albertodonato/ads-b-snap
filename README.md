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


## Connecting interfaces

After install, some snap interfaces need to be connected manually for the tools
to be able to access devices:


```bash
    sudo snap connect ads-b:raw-usb
    sudo snap connect ads-b:network-observe
```


## Enabling services

Services provided by the snap are disabled by default. After connecting
interfaces and the the SDR USB device, they can be started with

```bash
    sudo snap start --enable ads-b
```


## Snap configuration options

The snap has a few configuration options:

* `coord.lat`, `coord.lon`: GPS coordinates of the receiver
* `web.port`: TCP port for the web interface (default: `8080`)

Services are automatically restarted on configuration changes.
