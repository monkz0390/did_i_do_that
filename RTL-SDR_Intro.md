# RTL-SDR Intro
## What is an RTL-SDR
  RTL-SDR stands for "Realtek Software Defined Radio." It refers to a low-cost SDR receiver based on the Realtek RTL2832U demodulator chip, which was originally designed for receiving digital TV broadcasts but has been repurposed for general radio signal reception.
## Setting up the RTL-SDR
  **You will need**
  - RTL-SDR
    - included/compatible receiver antenna 
  - PC/laptop
    - 1 available USB-A Port
    - dual core processor
### TO_DO_LIST
  Make note of the version number of your RTL-SDR, in my case its V3
  on PC, navigate to [RTL-SDR Quick Start Guide](https://www.rtl-sdr.com/QSG)
  Quickstart guide will suggest a few articles depending on your device version number, such as
  - [x] [Quickstart Guide](#quickstart-guide): rtl-sdr.com/QSG - Current page. Helps you install the software and set up your dongle.
  - [x] [V3 Features Guide](#v3-features-guide): rtl-sdr.com/V3 - Learn how to use special V3 features like the direct sampling HF mode and bias tee.
  - [ ] [SDR# Users Guide](#sdr-users-guide): rtl-sdr.com/SDRSHARP - Learn about the settings in SDR#.
  - [ ] Dipole Antenna Guide: rtl-sdr.com/DIPOLE - Learn how to use your RTL-SDR Blog multipurpose dipole antenna (if purchased in set)

## Quickstart Guide
  - Beware of counterfits using the rtl-sdr name ([buying guide](https://www.rtl-sdr.com/store))
  - To get the most enjoyment out of RTL-SDR you will need a decent antenna.
    - [RTL-SDR antenna options](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)
    - [Wideband Discone Antenna](http://amzn.to/1PnZRQY)
    - [DIY Wideband Planar Disk Antenna(PDF)](http://www.wa5vjb.com/references/PlanarDiskAntennas.pdf)
  ### SDRSharp Setup Guide
  dSDR# is the most commonly used SDR program on Windows.fas
  - Must have Microsoft [.NET 8.0 x86 Desktop Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-8.0.6-windows-x86-installer) installed.
  - Must have Microsoft [Visual C++ redistributable](https://aka.ms/vs/17/release/vc_redist.x86.exe) installed.
  1. download sdrsharp-x86.zip from [airspy.com](http://www.airspy.com/download)
    - Do not download the community managed edition, as this is often broken.
  2. Extract (unzip) sdrsharp-x86.zip
  3. Double click on install-rtlsdr.bat from within the extracted folder.
  4. Plug in your dongle.
  5. find the file called zadig.exe. Right click this file and select "Run as administrator".
  6. In Zadig, go to "Options->List All Devices", uncheck "Ignore Hubs or Composite Parents".
  7. Select "Bulk-In, Interface (Interface 0)" from the drop down list.
>	:warning: WARNING: DO NOT select anything else or you will overwrite that device's driver! DO NOT click around randomly in Zadig. If you do you are likely to overwrite your mouse, keyboard, printer, soundcard etc drivers. Many bad reviews we get are due to people clicking around randomly in Zadig, so PLEASE check what you are doing first.
  8. Make sure the box to the right of the arrow shows WinUSB.
  9. Click Replace Driver.
  10. Open SDRSharp.dotnet8.exe and set the "Source" to 'RTL-SDR USB'.
    - smart screen warning might require unblocking the file
    - right file>properties> in general tab, check unblock>Apply>OK, try opening again
  11. Press the Play button(the right facing triangle in the top left of the program).
  12. Important! Don't forget to also adjust the RF gain settings by adjusting it in the Source window, in the lower left of SDR#. By default the RF gain is set at zero. A gain of zero will probably receive nothing but very strong broadcast FM - increase the gain until you start seeing other signals.

## V3 Features Guide
### Feature 1: Direct Sampling HF Mode
  This feature allows you to listen to HF signals between about 500 kHz to 28.8 MHz.

### Feature 2: Software Selectable Bias Tee
  ⚠️WARNING: Before using the bias tee please ensure that you understand that you should not use this option when the dongle is connected directly to a DC short circuited antenna unless you are using an LNA. Although the bias tee circuit is dual protected against accidental shorts with a thermal self-resetting fuse and overcurrent protection on the LDO, short circuiting the bias tee for an extended period of time (days) could damage the LDO or fuse permanently. Only use it while connected to an actual powered device, like an LNA, active antenna or the SpyVerter.

### Feature 3: Selectable Clock & Expansion Headers
  This is for advanced users who need to daisy chain clocks together for coherent experiments, or need to access other ports. You can either bridge the clock selector the directly with a solder bridge, or solder on a 1.27mm 2x2 header pin jumper.

### Feature 4: Additional GPIO Ports
  PCB has four GPIO's broken out and available [check this github](https://github.com/rfrht/FT991A-PAT/wiki/appendix-rtl-sdr-gpio)
  
## SDR# Users Guide
[link](https://www.rtl-sdr.com/sdrsharp-users-guide/)
![SDR# Start Screen Walkthough](https://www.rtl-sdr.com/wp-content/uploads/2018/05/sdrsharp_new.png)
### Startup First Steps
1. Increase the RF gain from zero to a higher value in the configure menu.
  - RF gain is the hardware amplification inside the RTL-SDR tuner (the “front end”) before the signal is digitized.
  - raise gain until signals become clearly visible, then back off a notch if the noise floor jumps a lot or you see overload symptoms.
2. Reduce the range slider on the right of the SDR# window to about -70 (for RTL-SDR dongles).
  - controls the display scale of the spectrum/waterfall (how many dB from top to bottom you’re viewing).
  - RTL-SDRs have modest dynamic range, so a ~70 dB visible span often gives a usable view where real signals pop out without the spectrum looking “flat” or “all noise.”
3. Enable the “Correct IQ” setting to remove the center spike if using an R820T/**R820T2**, or enable “Offset Tuning” in the configure menu if using an E4000/FC0012/13.
  - Many SDRs show a center spike (a line right at the tuned frequency). That’s usually not a real signal — it’s a “DC offset” / I/Q imbalance artifact from the hardware.
  - 
4. Turn off the “Snap to grid” setting, or adjust the PPM offset accordingly.
  - RTL-SDRs often have a small frequency error (crystal tolerance), and signals won’t land exactly where they “should.”
  - PPM is a correction factor that tells SDR# how far your dongle’s oscillator is off.
5. Set the 'Mode' to the correct setting for the signal that you are listing to.
  - “Mode” tells SDR# how to demodulate the signal (how to turn RF into audio/data).
  - NFM: Narrowband Frequency Modulation, info in small frequency shifts, voice and data
  - WFM: Wideband Frequency Modulation, large freq deviation, (broadcast FM radio)
  - AM: Amplitude Modulation, info in signal strength
  - DSB: Double Sideband, both sidebands, no assumptions
  - USB: Upper Sideband, Only the upper half of an AM signal spectrum, efficient AM variant, precise tuning
  - LSB: Lower Sideband, Only the lower half of an AM signal spectrum, mirror of USB
  - CW: Continuous Wave, it’s just a carrier being keyed heard as tone bursts. Morse (often use CW/USB with narrow filter)
  - RAW: The unprocessed I/Q samples. Recording unknown signals, Feeding external decoders, Reverse engineering protocols.

  - 
[ ] Figure out pluggins, find repo's, demos, instructions?
