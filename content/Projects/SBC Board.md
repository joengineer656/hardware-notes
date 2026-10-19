![[1768205407421.jpg]]
# The Idea
The idea of this board is to make a fully feacher Gate way (SBC Board) in PICO-ITX size or smaller compatible with Raspberry Pi shields
And make it fully open source
# Things I Need To Add 
- RK3576 CPU
- LPDDR5 Up to 16GByte
- RP2350A MCU
- 2 RJ-45 connector (with AVB/TSN Support)
- 2 Stack USB A Host
- UFS/eMMC connector for [external board from redxa](https://radxa.com/products/accessories/ufs-module/)
- Key E connector for wireless boards such as (I**Intel AX200 / AX210**, **MediaTek MT7921 / MT7922 / MT7925**, **RAK5166/RAK5167**)
- 40pin GPIO from RK3576 & 20pin from RP2350A
- Key M Connector for Nvme SSD
- MIPI (CSI, DCI) for cameras and display
- full size HDMI
- 2 UCB-C (RK3576 with OTG&DP, RP2350A)
- uSD Card soket
- Boot from UFS/eMMC, Nvme SSD, uSD card
- DC Jack for Power Up to 25v

# Schematics
## USB-C SOC
The USB-C will work as a USB-C3.2, Display Port, Power out

**the usb data & power**
![[Pasted image 20260921210529.png]]
![[Pasted image 20260921210546.png]]

in PD first the output is 5v to and after the negoyiation is complete the power level is work

**and with USBC DP**
![[Pasted image 20260921211204.png]]

the idea of connection all of them
but I don't need power Input and I have a MUX in the RK3576 
![[Pasted image 20260921213035.png]]
but need controller for PD and it will be **FUSB302BMPX**
and how negotiation work
![[Pasted image 20260923071556.png]]

and for the power input I don't need it, the power will take from dc jack connector, so I don't need power input
so we will search about load switch with enabel **TPS22953DQCR**
![[Pasted image 20260923070144.png]]

The USB C Connector
![[Pasted image 20260923070425.png]]

The idea of decoupling caps is to blocking the DC and throw the AC signal (data) 
"In applications that use AC coupling for interfacing the data converters, DAC outputs should be AC coupled using a 100 nF capacitor in package size 0402 or smaller. ADC can be AC coupled, if necessary, and should be 100 nF in package size 0402 or smaller"

![[Pasted image 20260923071033.png]]

![[Pasted image 20260923072051.png]]

and the usb **SUB (Secondary Bus pins)** these pins is for alt modes 
![[Pasted image 20260923072231.png]]
"In the type-C connector, the SBU or Secondary Bus pins are data paths for the DisplayPort AUX channel and hot plug detection (HPD). DisplayPort source and sink devices use the AUX Channel for device linking and management, while DP sink devices implement HPD with vendor-defined messages (VDM) to signal their presence or to request the attention of the DP source."

![[Pasted image 20260923072731.png]]

## USB-A Host
![[Pasted image 20260923074634.png]]
the same things as USBC SOC
and we add all of USB Host signals to USB Hub 
![[Pasted image 20260923074756.png]]

NOTE : USB A always the host and USB B/ Mico-B/ Mini-B always the device

the Idea of BPWR_DET & SPWR_DET:
The hub uses these two pins together to decide: _"Am I a self-powered hub or a bus-powered hub?"_ and reports that to the host during USB enumeration — which directly affects how much current the downstream ports are allowed to supply.
## HDMI
HDMI (High-Definition 
Media Interfaces)
**HDMI 2.0’s 18 Gbps to HDMI 2.1’s 48 Gbps data rates**

Differential pair routing must maintain 100Ω impedance with length matching within 5 mils for intra-pair traces and 10 mils between differential pairs.

![[Pasted image 20260924202511.png]]

The Idea of this section is to enable or fully disable the HDMI 
![[Pasted image 20260924202710.png]]
and for 1 transistor disable one pair of data
Why 220n ? 
![[Pasted image 20260924203222.png]]
![[Pasted image 20260924204355.png]]
## uSD Card
![[Pasted image 20260924205906.png]]

u may view the taller pins in the sd card and the idea of it to power the uSD Card first with VDD & VSS

u can use a SPI, 1 bit data, 4 bit data
![[Pasted image 20260924211313.png]]

what make u select one of these is the speed u want + the host u have 
![[Pasted image 20260924214348.png]]

SPI **Don't NEED** a pull ups but ths SD Mode need it

## Ethernet
![[Pasted image 20260924220814.png]]
and the MAC is in the MCU or SOC
MII : is for data
MDIO : is for controll (such as I2C but for ethernet)

POE (Power Over Ethernet) is to transfer power + data in the same wire (use in cameras to increse the cabels to it)
need some other component to trancfer the AC to DC

for crystal
![[Pasted image 20260924221728.png]]

## PCIe
in PCIe x1 is one line (1 dif TX + 1dif RX = 4 tracks)

the **PEWAKE** is used for wake up the M.2(device) from sleep mode
and the **CLKREQ** is used to generate clock from the host to the device

## Wireless
Key E for wireless modules

```embed
title: "M.2 Pinning | Embedded Artists Developer Site"
image: "https://developer.embeddedartists.com/assets/images/imx-int-pin_numbering-3ac9ef576999305818ba27958a92652c.png"
description: "This chapter presents the pinning used for the M.2 modules from Embedded Artists. It is essentially M.2 Key-E compliant with enhancements to support additional debug signals and 3.3V VDDIO override. The pin assignment for specific control and debug signals has been jointly defined by Embedded Artists, Murata, NXP and Infineon/Cypress."
url: "https://developer.embeddedartists.com/docs-m2/integration/pinning/"
favicon: ""
aspectRatio: "77.76049766718506"
```

This modules have many interface for connection PCIe&SDIO for WIFI or USB&UART for Bluetooth

The highest interface PCIe&USB is for the Very high speed modules in laptop
![[Pasted image 20260925144741.png]]

this modules use M.2 2230 standard

## UFS & eMMC
The Redxa UFS board use these connector 0513383474
```embed
title: "Radxa UFS Module"
image: "https://radxa.com/storage-expansion/ra022/thumb_radxa_ufs_module.webp"
description: "Compact. Detachable. UFS Redefined."
url: "https://radxa.com/products/accessories/ufs-module/"
favicon: ""
aspectRatio: "56.310679611650485"
```

we have UFS and eMMC, the UFS is faster, more security, more power efficient, more controll feature 

## MIPI
MIPI (Mobile Industry Processor Interface) is the stander for mobile
![[Pasted image 20260926203457.png]]

![[Pasted image 20260926203542.png]]
![[Pasted image 20260926203715.png]]

![[Pasted image 20260926222311.png]]

![[Pasted image 20260928151104.png]]
![[Pasted image 20260928151301.png]]


## LPDDR5


# Ideas
Add some LEDs OR Display
![[Pasted image 20260927002751.png|453]]

Board 40pin connector place 
![[Pasted image 20260918015307.png]]

M.2 Soket place 
![[Pasted image 20260918015459.png]]

from redxa Dragon Q8B
![[Pasted image 20260918195003.png]]
[Radxa Dragon q8b Schematic v1.30 | PDF](https://www.scribd.com/document/1057718768/Radxa-Dragon-q8b-Schematic-v1-30)

# Resources

```embed
title: "ROCK 4D | Radxa Docs"
image: "https://docs.radxa.com/img/rock4/4d/rock4d-top.webp"
description: "Product Overview"
url: "https://docs.radxa.com/en/rock4/rock4d"
favicon: ""
aspectRatio: "66.66666666666666"
```

```embed
title: "Radxa Dragon Q8B"
image: "https://radxa.com/dragon/q8b/thumb_radxa_dragon_q8b.webp"
description: "The Performance Foundation for Edge Intelligence"
url: "https://radxa.com/products/dragon/q8b/"
favicon: ""
aspectRatio: "56.310679611650485"
```
