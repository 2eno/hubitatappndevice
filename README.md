# tuya Generic RGBW Bulb for Hubitat (with protocol 3.5)

Local (LAN, no cloud) Hubitat driver for tuya based RGBW bulbs, supporting tuya protocol
versions 3.1, 3.3, 3.4 and **3.5**.

## Credits

This driver is the work of **Ivar Holand** ([ivarho/hubitatappndevice](https://github.com/ivarho/hubitatappndevice)),
licensed under the Apache License 2.0. This repository only packages that single driver for the
Hubitat Package Manager and adds tuya protocol 3.5 support. The 3.5 changes have also been
submitted upstream to ivarho/hubitatappndevice.

## Changes compared to the original

- tuya protocol 3.5: `00006699` frames with AES-GCM (12 byte IV, 16 byte tag, frame header as
  additional authenticated data) instead of `000055AA` frames with AES-ECB + HMAC
- 3.5 session key negotiation (same three-step handshake as 3.4, key derived with AES-GCM)
- AES-GCM built on top of AES/ECB, so no extra crypto classes are needed on the hub
- 3.5 test vectors in `DriverSelfTest`
- Fixed colour parsing and a division by zero in the HSL/HSV conversion

Tested with a LEDVANCE SMART+ WiFi Filament Edison RGBW bulb on protocol 3.5.

## Installation

- **Hubitat Package Manager:** search for "tuya Generic RGBW Bulb (protocol 3.5)", or install from URL:
  `https://raw.githubusercontent.com/2eno/hubitat-tuya-rgbw-bulb/main/packageManifest.json`
- **Manual:** Drivers Code → New Driver → Import:
  `https://raw.githubusercontent.com/2eno/hubitat-tuya-rgbw-bulb/main/Device/tuyaDevices/tuyaGenericBulbRGBW.groovy`

Configure the device IP, device ID, local key (e.g. from [tinytuya](https://github.com/jasonacox/tinytuya))
and select the protocol version of your bulb.

## License

Apache License 2.0, see [LICENSE](LICENSE).
