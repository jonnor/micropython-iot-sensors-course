

## TODO

Maybe

- Fill in some of the advanced topics
- Add section about Android. Can use Micro REPL app.

Later

- Windows fix with asyncio? Also add test. Not able to fix socket...
- Add diagrams showing the IoT topologies
- Update Wokwi diagrams to use compatible pinout for LED,MPU6050,analog
- Test micropython JIT in Wokwi
- Try ViperIDE in Firefox - new WebSerial??

## Windows issues

Windows. No asyncio packages!!
Was missing in manifest
Fix by https://github.com/ilovelinux

Windows. No socket module
https://github.com/micropython/micropython/pull/12810



## Mac OS Intel issues

From Vinicius Gubiani Ferreira
```
export CXXFLAGS="-std=c++14"
export LDFLAGS="-undefined dynamic_lookup -Wl,-all_load"
```
before the pip install seems to work, including when you start micropython.

Can't be 100% sure, since I used uv:
```
uv pip install micropython/ports/python --no-cache
```
NOTE: also had to "git clean -fdx" to ensure previous builds didn't leave garbage behind

Question: Does the prebuilt wheel packages in jonnor-micropython work for him?

## Interaction

Use the conference chat to share resources.
Back and forth.
Example. Send link to Wokwi sketches
Thread in Discord


## Notes


In the process we will covered the following:

- Doing basic physical input/output using GPIO. Analog and digital
- Reading digital sensors using I2C
- Storing/loading sensor data using on-board filesystem.
- Serving data and handling requests using MicroDot HTTP server
- Using browser with JavaScript for user interfaces
- Communicating with external servers using HTTP or MQTT

Key things but woven in

- Running locally with micropython binary
- Running on device with mpremote mounts
- Managing concurrent tasks using asyncio
- Installing libraries using mip package manager
- Persisting our application onto device. Copying files with mpremote

Mentioned in brief

- Automated testing, pytest style
- Using interrupts for high-priority work
- Execution time optimization using native/viper decorators (numba JIT style)
- Fast extensions using C modules
- Fast iteration of on-device code using mpremote mount

Out-of-scope

- Power management
- Bluetooth Low Energy
- IDE setup
- Type hinting and static checking with micropython-stubs and mypy 
- Developing drivers using I2C etc
- Driving actuators/motors etc
- Working with display/UI

IoT topologies

- Standalone device. Device acts as HTTP server, serves webui etc
- Many-to-many communication. Using a MQTT broker

MAYBE

- Using htmx or datastar for interactive UI driven from device-side MicroPython
- Client-side development in Python using PyScript + MicroPython

Doing development on-PC

- Emulate sensor on machine.I2C level?
https://github.com/planetinnovation/micropython-mock-machine
- Emulate sensor by a custom mocked class
- Use a separate asyncio task for generating the sensor data

Strategy

- Build up step by step
Start single file.
asyncio at the main, with tasks (initially one)

Take-aways

- asyncio is cooperative multitasking.
Delays will happen. Avoid holding loop too long. Yield.
