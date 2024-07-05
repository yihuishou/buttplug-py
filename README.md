# buttplug-py

[![PyPi version](https://img.shields.io/pypi/v/buttplug-py)](http://pypi.org/project/buttplug-py)
[![Python version](https://img.shields.io/pypi/pyversions/buttplug-py)](http://pypi.org/project/buttplug-py)
[![Discord](https://img.shields.io/discord/353303527587708932.svg?logo=discord)](https://discord.buttplug.io)

Buttplug-py is a python implementation of the Client of the Buttplug Sex Toy Control Protocol.
It allows users to write applications that can connect to Buttplug Servers, such as
[Intiface Central](https://github.com/intiface/intiface-central) or
[Intiface Engine](https://github.com/intiface/intiface-engine).

For more information on the Buttplug project, check out the project website at
[buttplug.io](https://buttplug.io).

## Officiality

Buttplug-py is not officially supported by the developers of Buttplug, it is a community maintained project.
There is an outdated official Python client that can be found in
[buttplugio/buttplug-py](https://github.com/buttplugio/buttplug-py).

## Table Of Contents

- [Support The Project](#support-the-project)
- [Documentation](#documentation)
- [Examples](#examples)
- [License](#license)
- [Changelog](#changelog)

## Support The Project

If you find this project helpful you can [support me via Ko-Fi](https://ko-fi.com/siegewizard).
Every donation helps to maintain this library up to date and adding new features.

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/siegewizard)

[Buttplug developer's Patreon](http://patreon.com/qdot) can be used if you wish to support the Buttplug project.

## Documentation

Currently, the documentation of the library is limited to class and methods documentations. The main entrypoint is the
Client class which will guide the reader forward.

## Examples

Example code is available in the examples/ directory. Examples are heavily commented to hopefully
make usage of the library clearer.

## License

Buttplug-py is BSD 3-Clause licensed. More information is available in the [LICENSE file](LICENSE).

## 记录一个远古版本的 Bug
需要确认这个版本是否已经修复了

#### send_vibrate_cmd(float) only works with single-motor devices
```
Devices with multiple motors will not vibrate as expected when using send_vibrate_cmd(float). Instead, only the first motor of that device will vibrate.

Steps to reproduce:

Connect a device with multiple motors (e.g. Lovense Edge)
Perform send_vibrate_cmd(1.0) on that device.
The first motor will vibrate while the second does not.
Expected behavior:

All motors will vibrate with the same intensity.

It appears to be because Line 255 of buttplug/client/client.py only sets the speed of the motor at index 0 and does not consider devices with multiple motors.

Workaround: Multiplying a list by the number of motors:
e.g.

vibratorCount = dev.allowed_messages["VibrateCmd"].feature_count
intensity = [1.0] * vibratorCount
await dev.send_vibrate_cmd(intensity)
```

## Changelog

The full changelog can be found [here](CHANGELOG.md).
