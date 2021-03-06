# Table of contents
  - [Disclaimer](#disclaimer)
  - [Importance of low input lag](#importance-of-low-input-lag)
  - [Physical setup](#physical-setup)
  - [Peripherals](#peripherals)
    - [Mouse](#mouse)
    - [Monitor](#monitor)
  - [BIOS](#bios)
  - [Hardware clocking](#hardware-clocking)
    - [CPU](#cpu)
    - [RAM](#ram)
    - [GPU](#gpu)
  - [Windows](#windows)
  - [Tools & resources](#tools--resources)
    - [Mouse](#mouse-1)
    - [Mousepad](#mousepad)
    - [Monitor](#monitor-1)
    - [PSU](#psu)
    - [CPU](#cpu-1)
    - [RAM](#ram-1)
    - [GPU](#gpu-1)
    - [Storage](#storage)
    - [BIOS](#bios-1)
    - [Windows](#windows-1)
    - [Alternatives to bloated programs](#alternatives-to-bloated-programs)
    - [Miscellaneous](#miscellaneous)
# Disclaimer
  - Due to the sheer complexity of hardware and software and differences between various architectures, your mileage may vary. However, it is useful to be aware of things that can impact user experience and adjust them according to your needs.
# Importance of low input lag
  - ["While participants performed dragging and scribbling tasks, very low levels of latency could be discriminated, i.e., ~1 versus 2 milliseconds while dragging"](https://www.semanticscholar.org/paper/In-the-blink-of-an-eye%3A-investigating-latency-Ng-Annett/386a15fd85c162b8e4ebb6023acdce9df2bd43ee)
  - [visual demonstration of 10 vs 1 milliseconds](https://www.youtube.com/watch?v=vOvQCPLkPt4&feature=youtu.be&t=80)
  - ["Why does system latency matter?"](https://www.nvidia.com/en-us/geforce/news/reflex-low-latency-platform/#why-does-system-latency-matter)
# Physical setup
  - [Issues](https://forums.blurbusters.com/viewtopic.php?t=6498) with [EMI](https://en.wikipedia.org/wiki/Electromagnetic_interference) and electricity can cause unintended behavior of electronic components, increasing input lag.
  - Make sure your outlets are properly grounded.
  - If you don't have enough outlets, buy a proper power strip ( < power conditioner < voltage regulator) and connect all devices directly to it. Only connect your hardware (no phone chargers and other stuff).
  - Disconnect all things you don't use from your motherboard. E.g. front USB, front audio, RGB, hard drive activity LED, system power LED, reset button etc.
  - Move all devices that have electric or electromagnetic fields away from your PC and peripherals. E.g. [router](https://www.theverge.com/circuitbreaker/2017/2/3/14496044/lg-ultrafine-5k-display-router-fix-redesign) ([example of a router with a high electric field](https://i.imgur.com/EIt51IX.jpeg)), power strip/conditioner, voltage regulator etc.
  - Make sure none of your cables are touching each other and untangle them. This applies to everything, including power and peripheral cables.
  - Check the USB layout of your system with [USB Device Tree Viewer](https://www.uwe-sieber.de/usbtreeview_e.html). Connect your mouse to the first port of the first controller (usually [this port](https://i.imgur.com/QGKAVoA.png)).
  - If your motherboard has multiple USB controllers, offload your other devices to them. Lower their polling rates to an acceptable level. E.g. your microphone doesn't need 1000 Hz
  - Test both HDMI and DP on each GPU port (don't Plug & Play these).
  - Keep your PC clean. Clogged heatsinks and dust filters will reduce airflow and consequently heat dissipation. Furthermore, ["dust may cause
electrical leakage, shorting and opening of PCBs under different conditions"](https://www.circuitinsight.com/pdf/impact_of_dust_ipc.pdf).
# Peripherals
  - ## Mouse
    - ### Wired vs. Wireless
      - The convenience of cordless mice is very appealing. However, there are significant drawbacks. Nowadays, [2.4 GHz](https://en.wikipedia.org/wiki/2.4_GHz_radio_use) is everywhere, causing a lot of interference. Additionally, aggressive [power saving mechanisms](https://i.imgur.com/5myJ46P.png) are implemented to increase battery life.
    - ### DPI
      - Depending on your preferred cm/360° in games, you may want to experiment with different DPI. Higher DPI [decreases latency](https://twitter.com/Chris_Pate/status/871307822562107394) and improves motion clarity. Most modern sensors are able to handle around 1600 DPI without sensor smoothing. To counteract the increased sensitivity on the Desktop and in game menus you can adjust the [Windows sensitivity](https://liquipedia.net/counterstrike/Mouse_Settings#Windows_Sensitivity).
  - ## Monitor
    - ### Capping FPS
      - [Input lag increases as GPU utilization increases](https://youtu.be/8ZRuFaFZh5M?t=817).
      - [Frame mistiming](https://youtu.be/_73gFgNrYVQ) causes severe stutters. To prevent this phenomenon you can cap your FPS at various values depending on your monitor's refresh rate. There are two formulae (X = monitor's refresh rate, Y = any integer):
        - X * Y
        - X / Y if X %Y = 0
      - These are some of the FPS cap values that will prevent mistiming:
        - 360 Hz: ... , 45, 60, 72, 90, 120, 180, 360, 720, 1080, ...
        - 280 Hz: ... , 40, 56, 70, 140, 280, 560, 840, 1120, ...
        - 240 Hz: ... , 48, 60, 80, 120, 240, 480, 720, 960, ...
        - 144 Hz: ... , 48, 72, 144, 288, 432, 576, 720, 864, 1008, ...
        - 120 Hz: ... , 40, 60, 120, 240, 360, 480, 600, 720, 840, 960, 1080, ...
# BIOS
  - Generally, follow the principle of "Don't use it? Disable it." E.g. disable all power saving features, unused network/audio/SATA controllers, unused USB/PCI/DIMM/SATA ports, RGB that can't physically be disconnected etc.
  - [How to change hidden settings without flashing a modded BIOS](https://github.com/BoringBoredom/IFR-Formatter)
  - ## Optimization guides
    - [Fujitsu guide](https://sp.ts.fujitsu.com/dmsp/Publications/public/wp-bios-settings-primergy-ww-en.pdf)
    - [r0ach's guide](https://www.overclock.net/threads/gaming-and-mouse-response-bios-optimization-guide-for-modern-pc-hardware.1433882/)
# Hardware clocking
  - I called this category *clocking* rather than *overclocking* because in the end all you do is run your silicon at its safe capabilities (which may not always be *over*clocking due to temperatures, for example).
  - [General Intel Lake clocking information](https://youtu.be/WK5Md-90XHQ)
  - [Core](https://youtu.be/WK5Md-90XHQ?t=851), [Uncore and RAM](https://youtu.be/WK5Md-90XHQ?t=1116) affect each other's stability, hence there is no definitive order.
  - ## CPU
    - Download the bootable version of [Linpack Xtreme](https://www.techpowerup.com/download/linpack-xtreme/) and mount it to a USB stick.
    - Set the [LLC](https://elmorlabs.com/index.php/2019-09-05/vrm-load-line-visualized/) to flat and adjust the VRM switching frequency. Generally, higher frequency results in more stable voltage at the cost of increased temperatures.
    - Boot into Linpack and stress test for a few minutes.
    - Monitor your temperatures and make sure you are below 80°C.
    - Continue raising both All Core and Uncore by 100 MHz and do quick stress tests. Eventually, you will either encounter instability or temperatures above 80°C.
    - If temperatures are too high, you can try lowering VCORE (P = I x V).
    - If you encounter instability, lower All Core and Uncore by 100 MHz and continue raising All Core from now on.
    - Ultimately, stress test for 2-4h to maximize long-term stability.
  - ## RAM
    - [Importance of memory clocking](https://kingfaris.co.uk/ram)
    - Dedicated cooling is advised since ["charge leakage rate of DRAM cells approximately doubles for every 10°C increase in the temperature"](https://www.pdl.cmu.edu/PDL-FTP/NVM/chargecache_low-latency-dram_hpca16.pdf).
    - [Integralfx's DDR4 guide](https://github.com/integralfx/MemTestHelper/blob/master/DDR4%20OC%20Guide.md)
  - ## GPU
    - [Cancerogeno's guide](https://docs.google.com/document/d/14ma-_Os3rNzio85yBemD-YSpF_1z75mZJz1UdzmW8GE/edit)
# Windows
  - I highly recommend setting up a multi-boot environment to separate the gaming and the "can-be-bloated" operating system. Keeping your programs and files on a different partition is also convenient due to both operating systems having shared access to everything and the ease of reinstalling either of them.
  - As usual, disable everything you don't explicitely need.
  - The Task Manager is a very inaccurate representation of system load since it only displays Core usage on a very superficial level. It doesn't account for things like [context switching](https://en.wikipedia.org/wiki/Context_switch) which can be very expensive. I recommend using [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) with [modified settings](https://github.com/BoringBoredom/PC-Optimization-Hub/blob/main/content/process_explorer_settings.reg) instead.
  - [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector) exposes a lot of settings that are hidden from the control panel.
  - Whenever possible, use portable versions of programs. Sometimes installers come with background services/drivers which may run even if the program is not running.
  - ## Optimization guides
    - [Calypto's guide](https://docs.google.com/document/d/1c2-lUJq74wuYK1WrA_bIvgb89dUN0sj8-hO3vqmrau4/edit)
    - [Timecard's guide](https://github.com/djdallmann/GamingPCSetup)
  - ## ISO creation
    - [Drivers](https://www.win-raid.com/f25-General-Storage-Drivers-AHCI-RAID-NVMe-and-USB.html) & [integration guide](https://www.win-raid.com/t750f25-Guide-Integration-of-drivers-into-a-Win-image.html)
    - [Rufus](https://github.com/pbatard/rufus)
    - ### ISO sources
      - [Heidoc](https://www.heidoc.net/joomla/technology-science/microsoft/67-microsoft-windows-iso-download-tool)
      - [Techbench](https://tb.rg-adguard.net/public.php)
      - [The Eye](https://the-eye.eu/public/MSDN/)
      - [DigitalRiver](https://digitalrivermirror.com/) (W7 only)
      - [KichHoatBanQuyen's list](https://docs.google.com/spreadsheets/d/14-D4tIlFp9APP0OOvQBRXvfLOYC447UygywenX5LXfo/edit)
# Tools & resources
  - ## Mouse
    - ### Documentation
      - [Newbrict's page](https://sensor.fyi/info/)
    - ### Tools
      - [Gearsearch shape comparison](https://gearsearch.gg/shape.html)
      - [RTINGS shape comparison](https://www.rtings.com/mouse/tools/3d-model-shape-compare/?orientation=3D)
  - ## Mousepad
    - [Hoya's comparison sheet](https://docs.google.com/spreadsheets/d/1RAnmZxDNduaGV8kB-GCvZ0MO6d9-0j9jmrU2f8dp0Ww/edit)
  - ## Monitor
    - ### Reviews
      - [RTINGS](https://www.rtings.com/monitor/reviews/best/by-usage/gaming#conclusion)
      - [TFT Central](https://www.tftcentral.co.uk/reviews_index.htm)
    - ### Tools
      - [Blur Busters' utilities](https://www.testufo.com/)
      - [EIZO monitor test](https://www.eizo.be/monitor-test/)
      - [Custom Resolution Utility](https://www.monitortests.com/forum/Thread-Custom-Resolution-Utility-CRU)
  - ## PSU
    - [Cybenetics](https://www.cybenetics.com/index.php?option=power-supplies)
    - [TechPowerUp](https://www.techpowerup.com/review/?category=Power+Supplies&manufacturer=&pp=25&order=date)
    - [Tom's Hardware](https://www.tomshardware.com/topics/power-supplies/reviews)
  - ## CPU
    - ### Documentation
      - [Intel resources](https://www.intel.com/content/www/us/en/products/docs/processors/core/core-technical-resources.html)
    - ### Tools
      - [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)
      - [Linpack Xtreme](https://www.techpowerup.com/download/linpack-xtreme/)
      - [Prime95](https://www.mersenne.org/download/)
  - ## RAM
    - ### Documentation
      - [DDR4 basics](https://www.systemverilog.io/)
      - [DDR4 JEDEC paper](http://www.softnology.biz/pdf/JESD79-4B.pdf)
    - ### Tools
      - [ASRock Timing Configurator 4.0.4](https://download.asrock.com/Utility/Formula/TimingConfigurator(v4.0.4).zip)
      - [ASUS MemTweakIt 2.02.48](https://cdn.discordapp.com/attachments/653171331256549386/755097007240249416/MemTweakIt_V20248.zip)
      - [Intel Memory Latency Checker](https://software.intel.com/content/www/us/en/develop/articles/intelr-memory-latency-checker.html)
      - [AIDA](https://www.aida64.com/downloads/NzI2ODhjM2U=)
      - [HCI MemTest](https://hcidesign.com/memtest/)
      - [Karhu RAM Test](https://www.karhusoftware.com/ramtest/)
      - [TestMem5](https://testmem.tz.ru/testmem5.htm) + [anta777's config](https://bit.ly/2MUvl6n)
      - [OCCT](https://www.ocbase.com/)
  - ## GPU
    - [Afterburner](https://www.msi.com/Landing/afterburner)
    - [NVIDIA NVFlash](https://www.techpowerup.com/download/nvidia-nvflash/)
    - [NVCleanstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/)
    - [NVSlimmer](https://forums.guru3d.com/threads/nvslimmer-nvidia-driver-slimming-utility.423072/)
    - [GPU-Z](https://www.techpowerup.com/gpuz/)
    - [Superposition](https://benchmark.unigine.com/superposition)
    - [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector)
    - [NVIDIA Nsight](https://developer.nvidia.com/nsight-graphics)
    - [NVIDIA FrameView](https://www.nvidia.com/en-us/geforce/technologies/frameview/)
    - [Furmark](https://geeks3d.com/furmark/)
  - ## Storage
    - ### Reviews
      - [TechPowerUp](https://www.techpowerup.com/review/?category=SSD&manufacturer=&pp=25&order=date)
      - [Tom's Hardware](https://www.tomshardware.com/topics/storage/reviews)
    - ### Tools
      - [WinDirStat](https://sourceforge.net/projects/windirstat/)
      - [Total Commander](https://www.ghisler.com/)
  - ## BIOS
    - [Win-Raid modding section](https://www.win-raid.com/f16-BIOS-Modding-Guides-and-Problems.html)
    - [Cancerogeno's compendium](https://sites.google.com/view/cancerogenoslab/bios-mods-and-tools)
  - ## Windows
    - ### Documentation
      - [Windows Internals](https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals)
    - ### Profiling / Monitoring / Benchmarking
      - [HWInfo](https://www.hwinfo.com/download/) + [LogViewer](https://www.hwinfo.com/forum/threads/logviewer-for-hwinfo-is-available.802/)
      - [CapFrameX](https://github.com/CXWorld/CapFrameX)
      - [Windows Performance Analyzer](https://docs.microsoft.com/en-us/windows-hardware/test/wpt/windows-performance-analyzer) ([all versions](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install))
      - [Intel VTune Profiler](https://software.intel.com/content/www/us/en/develop/tools/vtune-profiler.html)
      - [Mouse Tester](https://github.com/dobragab/MouseTester)
      - [Latencymon](https://www.resplendence.com/latencymon)
      - [Liblava](https://github.com/liblava/liblava-demo)
    - ### Tools
      - [Sysinternals](https://docs.microsoft.com/en-us/sysinternals/downloads/)  (huge compendium)
      - [Nirsoft's Tools](https://www.nirsoft.net/utils/index.html) (huge compendium)
      - [Process Lasso](https://bitsum.com/)
      - [Power Plan Settings Explorer](https://forums.guru3d.com/threads/windows-power-plan-settings-explorer-utility.416058/)
      - [Timer Resolution Service](https://forums.guru3d.com/threads/windows-timer-resolution-tool-in-form-of-system-service.376458/)
      - [NSudo](https://github.com/M2Team/NSudo)
      - [Compatibility Manager](https://github.com/Skymirrh/CompatibilityManager)
      - [Prio](https://www.prnwatch.com/prio/)
      - [VC++ Redist. AIO](https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/) (TPU)
      - [VC++ Redist. AIO](https://github.com/abbodi1406/vcredist) (abbodi1406)
      - [Quick CPU](https://coderbag.com/product/quickcpu)
      - [MSI Utility](https://forums.guru3d.com/threads/windows-line-based-vs-message-signaled-based-interrupts-msi-tool.378044/)
      - [Microsoft Interrupt Affinity Policy Tool](http://download.microsoft.com/download/9/2/0/9200a84d-6c21-4226-9922-57ef1dae939e/interrupt_affinity_policy_tool.msi)
      - [Device Remover](https://www.majorgeeks.com/files/details/device_remover_543c.html)
      - [USB Device Tree Viewer](https://www.uwe-sieber.de/usbtreeview_e.html)
      - [DeviceTree](https://www.osronline.com/article.cfm%5Earticle=97.htm)
  - ## Alternatives to bloated programs
    - Epic Games: [Legendary](https://github.com/derrod/legendary)
    - Spotify: [Foobar2000](https://www.foobar2000.org/)
    - Discord: [Ripcord](https://cancel.fm/ripcord/)
    - GHUB / LGS: [Logitech Onboard Memory Manager](https://download01.logi.com/web/ftp/pub/techsupport/gaming/Onboard%20Memory%20Manager.exe)
  - ## Miscellaneous
    - [Geizhals database](https://geizhals.eu/) (useful for finding specific hardware due to the very extensive filtering functionality)
    - [Virustotal](https://www.virustotal.com/gui/home/upload)
    - [Hybrid Analysis](https://www.hybrid-analysis.com/)
    - [NVIDIA article on lag reduction](https://www.nvidia.com/en-us/geforce/guides/system-latency-optimization-guide/)
    - [Ventoy](https://github.com/ventoy/Ventoy) (lets you create multi-boot USB drives)
# Keywords for Google indexing (ignore this)
input lag latency optimization performance gaming overclock windows ping debloat milliseconds fps boost increase decrease guide mouse tweak bios pc overclocking 7 8.1 8 10 w7 w8 w8.1 w10 game gamer optimizations frametime frametimes 0.1 1 average avg minimum maximum min max tweaking fortnite overwatch apex call of duty cs:go dota league of legends valorant rocket league rainbow six pubg tarkov rust starcraft destiny 2 OW FN COD LOL kovaak aim trainer krunker battlefield BF roblox delay delayed bloat bloated debloated steam battle origin epic games quake counter strike battle royale BR intel nvidia amd ryzen core i9 i7 i5 memory ram gpu ssd nvme
