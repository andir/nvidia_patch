nvidia_patch
============

some nvidia fixes i found usefull...

 - running 6x 27" screen each at 2560x1440 as one big X-Server (7680x2880) on 2x GTX680 (SLI-Mode), should be possible to even run 8 with 4 outputs per card but I only have 6 monitors
 
For version 331.49 you just need to change a single byte:
 0xb3e87 from 0x85 to 0x84
This changes a block looking like:
    test ah, 0x40
    jnz somewhere
to:
    test ah, 0x40
    jz somewhere

This works for my two 680's.


Notes for older/first version
=========

Be aware that i noop'ed out quiet a bit of the binary blob, some stuff is probably not nesscary but I'm happy to have it running at all...

To use this you'll have to patch the kernel module (the fake quadro patch should be enough) & apply changes to the binary as noted in nvidia_drv.dif


xorg.conf
==========


since nvidia-settings doesn't get tricked into allowing MosaicMode you'll have to edit the xorg.conf manually. Here is the important section I'm using:

    Section "Monitor"
        Identifier     "Monitor0"
        VendorName     "Unknown"
        ModelName      "DELL U2713HM"
        HorizSync       29.0 - 113.0
        VertRefresh     49.0 - 86.0
        Option         "DPMS"
    EndSection
    
    Section "Device"
        Identifier     "Device0"
        Driver         "nvidia"
        VendorName     "NVIDIA Corporation"
        BoardName      "GeForce GTX 680"
        BusID          "PCI:2:0:0"
    EndSection



    Section "Screen"
    
        Option         "SLI" "Mosaic"
        Identifier     "Screen0"
        Device         "Device0"
        Monitor        "Monitor0"
        DefaultDepth    24
        Option         "Stereo" "0"
        Option	   "MetaModes" "GPU-0.DVI-I-1: nvidia-auto-select @2560x1440 +2560+0 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}, GPU-0.DVI-D-0: nvidia-auto-select @2560x1440 +5120+0 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}, GPU-0.DP-1: nvidia-auto-select @2560x1440 +0+0 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}, GPU-1.DVI-I-1: nvidia-auto-select @2560x1440 +2560+1440 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}, GPU-1.DVI-D-0: nvidia-auto-select @2560x1440 +5120+1440 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}, GPU-1.DP-1: nvidia-auto-select @2560x1440 +0+1440 {ViewPortIn=2560x1440, ViewPortOut=2560x1440+0+0}"
        SubSection     "Display"
            Depth       24
        EndSubSection
  
  
    EndSection


