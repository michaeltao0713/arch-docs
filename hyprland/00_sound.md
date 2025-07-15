# Sound

Follow the Advanced Linux Sound Architecture (ALSA) wiki page. Honestly, just the first section really.

ALSA should have already been installed with the linux kernel. If you're on laptop and can't hear sound, install sof-firmware.

For basic audio management, install alsa-utils and run alsamixer.

### Sound Manager GUI
You'll probably want a GUI for switching audio devices and changing volume and muting applications quickly. Check out the [Sound System](https://wiki.archlinux.org/title/Sound_system) wiki for Sound Server options.

I'm going to go with PipeWire probably. It's newer and aims to replace JACK and PulseAudio which were the previous favorites. Since I'm going to using Hyrpland, it also recommends using Pipewire with Wireplumber session manager. PipeWire is also used for screensharing.

Install pipewire and wireplumber. Again, if you're using steam, good idea to install lib32-pipewire too. Also install pipewire-pulse, pipewire-alsa and pipewire-jack so that pipewire can run for applications reliant on PulseAudio, ALSA and JACK respectively.

Wireplumber is a session manager that allows PipeWire to watch for new streams and connect. It is the recommended session manager.

Consider a GUI as well, for volume sliders and ability to mute certain sources of sound. I recommend pavucontrol, the default sound GUI for GNOME.

### Configuration
Not much, you can configure default devices in the pavucontrol menu by opening it via terminal or application manager.
Your volume control macros should also work automatically.


Could look into "Echo Cancellation" from https://wiki.archlinux.org/title/PipeWire/Examples#EchoCancellation
