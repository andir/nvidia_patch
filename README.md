nvidia_patch
============

some nvidia fixes i found usefull...

 - running 6x 27" screen each at 2560x1440 as one big X-Server (7680x2880), should be possible to even run 8 with 4 outputs per card but I only have 6 monitors
 
Be aware that i noop'ed out quiet a bit of the binary blob, some stuff is probably not nesscary but I'm happy to have it running at all...

To use this you'll have to patch the kernel module (the fake quadro patch should be enough) & apply changes to the binary as noted in nvidia_drv.dif
