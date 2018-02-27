# setaudio
A simple launchd plist to set a usb audio device output, automatically, when the device is attached. This plist makes use of whosawhatsis's handy utility [audiodevice](http://whoshacks.blogspot.com/2009/01/change-audio-devices-via-shell-script.html). This can solve the problem of a Mac laptop staying on internal speaker output, even when docked.

## Customization

By default, this is set up for detecting an [Elgato Thunderbolt 3 dock](https://www.elgato.com/en/dock/thunderbolt-3) (which includes a USB-based audio input and output). If you're using a different USB audio device, you will want to edit the .plist to match your device.

1. Change the last `ProgramArguments` string (specifically, the last argument of the `audiodevice` program) to match the exact name of the audio output you want to use. In my case it's **Elgato Dock** (note that this is the name given to the device by the Elgato Dock utility; if you own this dock but haven't installed the utility, the name is **USB Audio CODEC**). Also remember to escape spaces with a backslash (as in `Elgato\ Dock`)

2. Change the `idProduct` and `idVendor` integers to match the device. This can be found in the **System Information** app, under USB (or, `ioreg -p IOUSB` in Terminal).

3. Change the `IOProviderClass` string to match the device. This can also be found by running `ioreg -p IOUSB` in Terminal. For the Elgato dock it's `AppleUSBDevice` but yours may be different.

Once you're certain you have the right values in the plist, you're ready to install.

## Installation

1. Move the `com.eoban.setaudio.plist` file to `~/Library/LaunchAgents/`

2. Run `launchctl load ~/Library/LaunchAgents/com.eoban.setaudio.plist`

3. Move the `Audiodevice` directory to `/Applications/`.

## Use

The program should now run automatically in the background when your audio device is plugged in.