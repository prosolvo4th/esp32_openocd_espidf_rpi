ESP32, ESP-IDF, RaspberryPi and OpenOCD
=

This instruction based on info found in free access in web and describes
setting-up dev and debug setup on RaspberryPi 3B using ESP-IDF, OpenOCD and RaspberryPi GPIOS as debug interfaces. 

Setup RaspberryPi OS (64-bit)
-
Nothing special, just flash micro SD card and insert it in your RaspberryPi.
It is useful to use RaspberryPi Imager, which allow preset new user, enable sshd by default and setup WIFI.

![RaspberryPiImager settings](RaspberryPiImager.PNG "")

It is also might be handy to enable USART as fallback method to connect.
Just add lines int the end of config.txt

	# Enable UART
	enable_uart=1

Setup ESP-IDF
-
ESPRESSIF has good enough documentation. Just follow the instructions: [Standard Toolchain Setup for Linux and macOS](https://docs.espressif.com/projects/esp-idf/en/v5.1.1/esp32/get-started/linux-macos-setup.html).
The only recommenation: do not add permanently exporting envorionment by adding the next line to your `.bashrc`.
Instead, add alias:

	alias get_idf=". $HOME/esp/esp-idf/export.sh ; PS1=\"(ESP-IDF)$PS1\""

Setup OpenOCD
-
Thanks to Uri Shaked, we easely can use his instructions to setup jtag debug by bare pins on RaspberryPi.
[ESP32 JTAG Debugging using Raspberry Pi](https://blog.wokwi.com/gdb-debugging-esp32-using-raspberry-pi/).

Notes:
- using `bcm2835gpio_jtag_nums 11 25 10 9` is depricated, instead use:
	- `adapter gpio tck 11`
	- `adapter gpio tms 8`
	- `adapter gpio tdi 10`
	- `adapter gpio tdo 9`
- due to change `tms` from `25` to `8`, wiring will be slightly different. Check pinout.

![RaspberryPi pinout](RPiGPIO.PNG)

- `adapter_khz` is depricated, use `adapter speed`
- better to not install openocd globally

