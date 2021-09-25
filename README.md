# Deskmini-H470-Opencore-EFI
This is an efi boot sample file for deskmini h470 on opencore 7.3

| Harware  |      My Setup |  comment |
|----------|:-------------:|------:|
| MotherBoard |  Asrock H470-stx | All in one mini PC |
| CPU |    intel i3-10100   |   Comet lake processor |
| CPU cooler| ID-cooling IS-40x | Need to lift the case when installing, fan works without hitting the case|
| GPU | Intergrated UHD630 | Supports up to 3 displays |
| RAM |  Crucial DDR4 3200 8GB SODIMM x2 | Overspect as  |
| Storsage |    Cruicial P5 Nvme 1tb | picker to login in 13ish seconds |
| Wifi/Bluetooth | BCM94352Z/DW1560 | sidecar and airdrop works |

# Hackintosh
HDMI and DP boots, type c not rested
Powermanagement

# Known issues
1. When booting with dual screen on, horizontal stripes/artifacts appears on screen which can be solved by repluging the moniter or turn on screen after login
2. Popping/ hissing sound for certain speakers when booting, shutting down or sleeping, no issues when using macOS


# To be done in future
1. Bulid my own SSDTs

# Debugging 
1. Reset NVRAM
