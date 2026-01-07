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
  - [ ] [Quickstart Guide](#quickstart-guide): rtl-sdr.com/QSG - Current page. Helps you install the software and set up your dongle.
  - [ ] V3 Features Guide: rtl-sdr.com/V3 - Learn how to use special V3 features like the direct sampling HF mode and bias tee.
  - [ ] V4 Features Guide: rtl-sdr.com/V4 - Learn how to use special V4 features and how to install the required drivers for V4 models.
  - [ ] SDR# Users Guide: rtl-sdr.com/SDRSHARP - Learn about the settings in SDR#.
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

  
