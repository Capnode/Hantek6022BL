# Hantek 6022BL

I was looking for an USB oscilloscope that was not too expensive but still equipped with nice features for my Arduino projects. I found the Hantek 6022. There are two models: 6022BE with 2 analog channels and the 6022BL with 2 analog channels and also 16 digital channels for a logic analyzer. I ordered two 6022BL to see if they can be used at the same time. On the back of the 6022BL is a swich button to select operation mode: oscilloscope (H) and logic analyzer (P). It can not operate as both at the same time on a single device. The Hantek 6022BL comes with oscilloscope and logic analyser software, but there are alternatives: [Six Software Apps To Use With The Hantek 6022BE - an Overview](https://rudysmodelrailway.wordpress.com/2019/09/13/hantek-6022be-usb-oscilloscope-and-6-scope-software-apps-to-go-with-it/) has listed six alternatives of which four still remains.

## HScope
[HScope](https://www.martinloren.com/hscope-guide/) is an Android app with a very nice user interface that connects to the Hantek device and can be installed from Google Play.

## Hantek
The original software from [Hantek](https://www.hantek.com/products/detail/153) for oscilloscope and logic analyser for Windows. The oscilloscope software supports multiple instances and with two Hantek devices it is possible to run two oscilloscopes in parallel, four channels in total. However the logic analyzer software is more limited and does not support multiple instances. There is also an issue with the USB driver that does not install on Windows 11 unless you deactivate the memory protection in Windows 11.

## OpenHantek6022
[OpenHantek6022](https://github.com/OpenHantek/OpenHantek6022) is an open source oscilloscope software that supports Linux, Mac and Windows. It supports multiple instances of the oscilloscope software to run in parallel. The USB driver supports Windows 11 and also includes an USB driver for the logic analyzer, however software for the logic analyzer is not included and it is recommended to use sigrok/pulseview.

### Install instructions for OpenHantek6022 on Windows
1. Download the latest release of [OpenHantek](https://github.com/OpenHantek/OpenHantek6022/releases).
1. Extract the zip file to a location of your choice.
1. Plug in the device and make sure it can be found in the Device Manager under Other devices as an Unknown device. Uninstall any other Hantek 6022 device already installed.
1. Install USB driver from the driver folder. Right-click on `OpenHantek.inf` and select "install" from the pull-down menu.
1. Make sure the push button on the back of the Hantek 6022BL is in the inner position marked "H".
1. Unplug and insert the USB cable to restart the device.
1. Start the software named `OpenHantek.exe`. The device is now located and the firmware is reloaded after power on.

## PulseView
PulseView from [sigrok](https://sigrok.org) provides two logic analyzer tools for Linux, Mac and Windows. PulseView has a graphical user interface while sigrok-cli is command line based. PulseView supports running multiple instances in parallel. There are some difficulties to make PulseView work with the USB driver, especially with all [16 digital channels](https://www.eevblog.com/forum/testgear/hantek-6022bl-logic-analyzer-working-with-sigrok-all-16-channels/). Follow the instructions below to make it work.

### Install instructions for PulseView on Windows
1. Install the USB driver as described for OpenHantek6022.
1. Download and execute the [PulseView](https://sigrok.org/wiki/Downloads) installer.
1. Make sure the push button on the back of the device is in out position (P) and restart the device.
1. Start PulseView from the Start menu.
1. PulseView now starts with `<No Device>` selected, but with one new device created under Other units in the Device Manager. It is named `fx2lafw` and is marked with an exclamation mark. Terminate PulseView.
1. Start the program Zadig (Pulseview) from the start menu.
1. Zadig starts with the device `fx2lafw` selected. Press Install Driver to install the WinUSB driver on the device.
1. Find PulseView firmware folder at `C:\Program Files\sigrok\PulseView\share\sigrok-firmware`.
1. Rename the file `fx2lafw-saleae-logic.fw` to `fx2lafw-saleae-logic.fw.bak`
1. Create a copy of the file `fx2lafw-sigrok-fx2-16ch.fw` and rename it to `fx2lafw-saleae-logic.fw`.
1. Unplug and insert the USB cable to restart the device.
1. Start PulseView and it will hopefully find all 16 channels.


