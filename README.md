# LEDVANCE RGBW Bulb for Hubitat (tuya local, protocol 3.5)

Local (LAN, no cloud) Hubitat driver for **LEDVANCE SMART+ WiFi** RGBW bulbs and other
tuya based RGBW bulbs. LEDVANCE WiFi bulbs run on the tuya platform, so this driver talks to
them directly with the tuya local protocol, versions 3.1, 3.3, 3.4 and **3.5**.

## Credits

This driver is the work of **Ivar Holand** ([ivarho/hubitatappndevice](https://github.com/ivarho/hubitatappndevice)),
licensed under the Apache License 2.0. This repository only packages that single driver (originally named
"tuya Generic RGBW Bulb") for the Hubitat Package Manager and adds tuya protocol 3.5 support. The 3.5 changes have also been
submitted upstream to ivarho/hubitatappndevice.

## Acknowledgements

- [TinyTuya](https://github.com/jasonacox/tinytuya) by Jason Cox (MIT License): the protocol 3.5
  implementation follows TinyTuya's behaviour, and TinyTuya was used to generate the 3.5 test
  vectors in `DriverSelfTest`. It is also the recommended tool to find the device ID, local key
  and protocol version of your bulb. No TinyTuya source code is included in this driver.

## Changes compared to the original

- tuya protocol 3.5: `00006699` frames with AES-GCM (12 byte IV, 16 byte tag, frame header as
  additional authenticated data) instead of `000055AA` frames with AES-ECB + HMAC
- 3.5 session key negotiation (same three-step handshake as 3.4, key derived with AES-GCM)
- AES-GCM built on top of AES/ECB, so no extra crypto classes are needed on the hub
- 3.5 test vectors in `DriverSelfTest`
- Fixed colour parsing and a division by zero in the HSL/HSV conversion
- Driver renamed to "LEDVANCE RGBW Bulb (tuya)"

Tested with a LEDVANCE SMART+ WiFi Filament Edison RGBW bulb on protocol 3.5.

## Installation

- **Hubitat Package Manager:** search for "LEDVANCE" or "tuya", or install from URL:
  `https://raw.githubusercontent.com/2eno/hubitat-ledvance-rgbw-bulb/main/packageManifest.json`
- **Manual:** Drivers Code → New Driver → Import:
  `https://raw.githubusercontent.com/2eno/hubitat-ledvance-rgbw-bulb/main/Device/tuyaDevices/tuyaGenericBulbRGBW.groovy`

Configure the device IP, device ID, local key (e.g. from [tinytuya](https://github.com/jasonacox/tinytuya))
and select the protocol version of your bulb.

## License

Apache License 2.0, see [LICENSE](LICENSE).
