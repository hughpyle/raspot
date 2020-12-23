# Hugh's raspotify config

This repo contains the configuration files for the living-room stereo.

## Hardware

Loudspeakers are early-70s [Bose 901 Series II](http://cabezal.com/pix/901-minidsp-ucd/owg_en_901_series2.pdf).  These need some quite dramatic EQ, which originally would
be done with the [Bose equalizer box](http://cabezal.com/pix/901-minidsp-ucd/Bose-901-III-equal.pdf), but I'm using DSP software instead.

Amplifier is a [Wadia 151](http://www.wadia.com/ContentsFiles/151_Tech_Sheet%20web.pdf), which is basically a very nice USB DAC power-amp.

The source is a Raspberry Pi.

## Software

For now, the only music source is Spotify.  Using [raspotify](https://github.com/dtcooper/raspotify),
the Raspberry Pi shows up as a Spotify Connect device.

Playback is then routed via [CamillaDSP](https://github.com/HEnquist/camilladsp) to apply EQ for the loudspeakers.  The setup steps are really nicely documented [here](https://github.com/HEnquist/camilladsp-config)

* The `/etc/default/raspotify` [configuration file](https://github.com/hughpyle/raspot/blob/master/var_cache_raspotify/etc_default_raspotify) sets up 'raspotify' to play to the 'loopback' ALSA device, and adds an event handler (for notification when the track changes -- later).

* The `/lib/systemd/system/raspotify.service` [configuration file](https://github.com/hughpyle/raspot/blob/master/var_cache_raspotify/lib_systemd_system_raspotify.service) sets all the environment variables and parameters to run 'raspotify' as a service.

* The `/var/cache/raspotify` directory has the `camilladsp` executable and [configuration file](https://github.com/hughpyle/raspot/blob/master/var_cache_raspotify/dsp.conf). The DSP config in this case includes various hand-crafted artisanal IIR (biquad) filter settings to make the loudspeakers sound the way I want them to.

* The `/var/cache/raspotify/event` [script](https://github.com/hughpyle/raspot/blob/master/var_cache_raspotify/event) is work-in-progress...
