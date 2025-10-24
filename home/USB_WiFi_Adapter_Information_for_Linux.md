## USB WiFi Adapter Information for Linux

> [!CAUTION]
> The authors and contributors to this site cannot be responsible for the results of your use of the information contained in or linked from this site.
> We attempt to provide accurate information but many factors that are beyond our control can contribute to less than expected results.
> You are responsible for ensuring the accuracy and applicability of any information you use to make a decision.

If you are interested in USB WiFi information for Linux, you have come to the right place. This little github site started some years ago in an effort to help Linux users with information that would help them make informed choices about what USB WiFi adapters would work best for them. The site has grown over the years and many thousands of Linux users stop by every month. While here, users will discover that wireless networking support in Linux has improved dramatically over the last 5-7 years. The information here shows many products that work really well with Linux. We hope that the improvements to Linux wireless support continue into the future but until there is universal excellent support, it is important to be informed before buying wireless products.

There are many USB WiFi adapters that work without the need to install a driver in Linux.
[These adapters](./USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md) use drivers that are already in the Linux kernel.
The in-kernel drivers are maintained in the kernel without the need for user intervention.
With adapters that use in-kernel drivers, simply plug the adapter in and it will work (applies to most desktop/laptop distros as many server distros do not include WiFi support but it can be added).
Many people find that using adapters with in-kernel drivers is a better solution than using an adapter that requires drivers to be found (not easy to find the right driver), downloaded, compiled (confusing for those that are not developers) and installed (problematic, depending on the Linux distro and other factors).

### Internal Cards vs USB Adapters

USB WiFi adapters provide more flexibility than internal cards as they can be easily moved from one location to another and from one computer to another and can even be taken on the road. They come in models for USB 2 and USB 3 and often provide better reception than internal WiFi cards. Some of the larger adapters work well for desktop use and the smaller adapters, including "nano" adapters, work well for laptops and travel.

It is important that you pick an adapter to match the expected usage. If you are going to be traveling with the adapter, the adapters with long antennas may not work well since the adapter may be broken. Many adapters with large antennas allow you to remove the antennas for travel but then you will have more things to keep track of.

On the other hand, if you need an adapter for a desktop system that is a long distance from the AP/WiFi Router in your home or workplace, you probably need the better signal capability of the larger antennas. I realize that I am making it sound like large antennas always provide better range but that is not the case. Adapter makers pick their own antennas and amps to pair with the chipsets and there can be a lot of difference in the quality of the antennas and amps that are used so asking questions and researching is required to make sure you get what you are looking for.

### Linux Drivers

USB WiFi is viewed by the makers of WiFi hardware as a niche market within the WiFi industry. Many WiFi hardware makers do not supply USB WiFi chipsets. This means that choice is more limited than with other computer-related product lines.

There are only 3 companies currently supplying chipsets for USB WiFi adapters - [Mediatek](http://www.mediatek.com/), [AIC Semiconductor](https://www.aicsemi.com/) and [Realtek](https://www.realtek.com/).
Intel does not supply USB capable chipsets and Qualcomm-Atheros is not supplying modern USB capable chipsets.
Of the suppliers that do provide USB WiFi chipsets, Mediatek supports drivers for their chipsets the right way, in-kernel. Mediatek drivers are Linux Wireless Standards compliant (mac80211) and are updated and improved constantly without users having to worry about it.

#### Tips

1. It is common for online retailers to post "Linux support."
   It is best to ignore "Linux support" in online ads as this statement is often misleading at best and false at worst.
1. Most inexperienced users do not understand that the Linux kernel is under constant development which makes it necessary for drivers to be regularly updated in order to work on newer kernels.
   Out-of-kernel drivers sitting on a CD or on an adapter seller's web site do not get regular updates.
1. Rule of thumb: Never attempt to install a Linux driver from a CD.
   Only consider downloading a Linux driver from an adapter seller's website if you confirm it supports the kernel you are using.
   The out-of-kernel drivers on that CD or seller's webisite will likely be old and will likely do nothing more than make a mess of your system.
1. Remember that `sudo` is a weapon of mass destruction if used without knowing what you are doing.
1. Don't take hardware advice from Windows or macOS users, as support for either of those operating systems does not necessarily translate to Linux support.
1. All major Linux distributions have active forums with users ready to give advice.
1. Do not take advice from a single user.
   Instead, seek advice from several users and always ask if the adapter uses in-kernel drivers.

#### Realtek USB Support

Edit: 2025-06-31, the below statements about Realtek WiFi 6 and WiFi 7 driver support will likely be modified by the end of this year as a lot of progress has been made by a group of community developers. If you want to see the new drivers, test them or use them:

https://github.com/morrownr/rtw89

Realtek does _not_ support their WiFi 6 USB WiFi chipsets with in-kernel drivers and it does not currently provide any Linux support for its WiFi 7 USB WiFi chipsets. My current recommendation is for Linux users to avoid Realtek WiFi 6 and 7 based USB WiFi adapters and modules as Standards Compliant drivers could be years out.
Most Realtek WiFi 5 USB WiFi adapters are supported by good in-kernel drivers provided by the community. This support is in the mainline kernel as of kernel 6.14 for most WiFi 5 chips and 6.16 for the rtl8814au chip. If you are not yet using a distro with kernel 6.14 and you want to install this updated driver support, see [rtw88](https://github.com/lwfinger/rtw88).

Am I a fan of how the Realtek USB team supports the Linux community? No.

Users of the Realtek out-of-kernel drivers that are maintained at this site frequently ask some variant of the following question:

> Why don't you submit \<insert Realtek driver\> to be included in the Linux kernel?

The Realtek out-of-kernel drivers are not Linux Wireless Standards compliant and will not be accepted into the Linux kernel.

> [!NOTE]
> While there are Realtek out-of-kernel drivers maintained at this site, this should _not_ be seen as recommendation for Linux users to buy USB WiFi adapters that use the out-of-kernel drivers.
> Realtek out-of-kernel WiFi drivers, such as the ones maintained here, are designed to be used by skilled programmers producing products such as embedded systems.
> Users of desktop distros such as Ubuntu, Debian, Manjaro, Fedora, Raspberry Pi OS and other mainline desktop distros will likely find adapters that use in-kernel drivers to be more stable, much more trouble-free and more feature rich.
> More information is available [here](./USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md).

#### TP-Link and D-Link

I will list products made by TP-Link and D-Link in The Plug and Play List by exception only.
Both companies regularly change chipsets while keeping the same model number on their products.
This makes it very difficult for Linux users to identify products with a specific chipset with any degree of certainty.

This also makes it difficult for me to post links and recommendations so I will not do so but that is okay because there are many good adapters available from other companies such as Alfa, Panda, Edup and others.
TP-Link and D-Link's Linux support is very poor as their product support sites generally only contain very old Linux drivers that won't work with modern distros... if they post any drivers at all.
Neither company does a good job of supplying adapters that use in-kernel drivers.

We know that Linux cannot be properly supported in the manner that both companies use.
This is sad because both companies have made a lot of money from Linux by using it inside many of their products, yet they do not return the support.
My recommendation is to avoid TP-Link and D-Link USB WiFi adapters.

Additionally: There is a lot of evidence that TP-Link does not abide by the GPL and other open source licences that they have accepted by using Linux in their products.
In my opinion, this is unacceptable and I STRONGLY recommend that Linux users worldwide refuse to purchase any TP-Link product until this situation is corrected.

#### Onboard Windows Drivers (multi-state adapters)

Some USB WiFi adapters have proprietary Windows drivers onboard.
When plugged in, they act like a flash drive or CDROM and on Windows will attempt to start installing the Windows driver.
That won't work on Linux, macOS or any other non-Windows OS so the adapter sits there in flash drive or CDROM mode.
The problem is that the state of the adapter has to be changed for the adapter to show up as the device that you expect, in this case, a WiFi adapter.

Most modern Linux distributions ship with a utility called [usb-modeswitch](./How_to_Modeswitch.md) that will handle this issue for you if it has the correct information for your adapter.
It is a good utility and works well most of the time, but if you buy adapters that are "multi-state," that is one more potential headache you may have to deal with when something goes wrong.
Often you can identify adapters that are "multi-state" as they are advertised as "free driver" or "free installation driver."
If you are looking to buy a USB WiFi adapter for use on Linux, macOS, UNIX or anything besides Windows, it is a good idea to give preference to single-state adapters. In fact, I recommend that Windows users avoid these multi-state adapters because the onboard drivers are not updated as time passes and new versions of Windows are released. This is a potential source of problems.

#### Recommendations

Buy adapters based on chipsets from the company that is doing it right - Mediatek.
The biggest problem most Linux users have when looking to purchase a USB WiFi adapter is being able to reliably identify which adapters have in-kernel support and that is the primary reason for this site.
Spreading this information far and wide is key to having happy Linux users so please spread this information.

[This document](./USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md) attempts to identify currently available adapters that use in-kernel driver support.
Links are provided to online products.
Information regarding out-of-kernel drivers and their quality is also provided in a [separate document](./USB_WiFi_Adapter_out-of-kernel_drivers_for_Linux.md).
The hope is that this information is of benefit to Linux users, experienced and new.

[Linux Wireless - Mediatek](https://wireless.wiki.kernel.org/en/users/drivers/mediatek) is a good place to get an idea of the various Mediatek WiFi chipsets that are supported in the Linux kernel.
If you want to look in the kernel to see the drivers, [look here](https://github.com/torvalds/linux/tree/master/drivers/net/wireless/mediatek).
One of the biggest advantages of using adapters with in-kernel drivers is that any of us can report [bugs](https://wireless.wiki.kernel.org/en/users/documentation/reporting_bugs) and submit fixes.
I recommend that you report bugs/issues here in 'Issues' before taking the problem to the kernel devs as they are very busy and may ignore your report if the issue is not worked to the point where it is highly likely the problem is something that requires a code change in the kernel drivers.

I have to give a shout out to 2 companies that do an excellent job making adapters that work well with Linux: Alfa and Panda.

- Alfa makes very high quality adapters.
  - Selected adapters use in-kernel drivers.
  - They have Linux information on their website which provides tech support and links to out-of-kernel drivers for the adapters that do not use an in-kernel driver.
- Panda has a long history of only making USB adapters that use Linux in-kernel drivers.

It is hard to go wrong with USB WiFi adapters from either company.
It is worth researching to find adapter sellers that sell Alfa and Panda adapters. I recommend that you use The Plug and Play List to see the recommended Alfa and Panda adapters.

### WPA3-SAE Support

My testing over the last few years has shown very positive results for WPA3 as far as in-kernel drivers are concerned.
I have tested USB WiFi adapters ranging from N150 to AXE3000.
It appears that all of the adapters that use Mediatek/Ralink and Atheros chipsets and in-kernel drivers are working well regarding WPA3.
Keep in mind that your Linux distro must support WPA3 for WPA3 to work.
As of mid-2022, all distros that I use and test with are working well with WPA3.
This includes Ubuntu 22.04 LTS and later as well as all of the official and unofficial versions of Ubuntu.
Most modern out-of-kernel drivers (Realtek) do support WPA3-SAE now.

### USB Extension Cables and Adapters

USB extension cables with cradles can be very useful with USB WiFi adapters as they will allow you to position the adapter for best performance.
Cables for USB2 and USB3 are available.
The following cables are not recommended but are shown as examples:

[StarTech.com 5ft USB 2.0 Extension Cable](https://www.amazon.com/5ft-Desktop-USB-Extension-Cable/dp/B001K9BFB8)

[Cablecc USB 3.0 Type-A Male to Female Extension Dock Station Docking Cable](https://www.amazon.com/Cablecc-Female-Extension-Station-Docking/dp/B07SH4RZ6S)

[WiFi Adapter Extension Cable with Pedestal](https://smile.amazon.com/gp/product/B08R2Y53QK?ref=em_1p_0_im&ref_=pe_3681270_598503160)

> [!NOTE]
> Some adapters won't work with some extension cables and cradles.
> It is best to buy from retailers that will let you return their products as it seems the only way to know is trial and error.

[Right angle usb adapters](https://www.amazon.com/dp/B07S6B5X76) can be very handy when using USB WiFi adapters.
This is especially true if you are using a Raspberry Pi or other small systems with horizontal usb ports.
Unlike extension cables, I have never seen a compatibility problem with right angle usb adapters.

> [!WARNING]
> USB3 cables and connections can cause interference with 2.4 GHz WiFi and Bluetooth.
> This interference can be really bad if operating external high speed storage on USB3.
> It would be best to keep your WiFi adapter away from the USB3 cables connected to high speed storage. It could be better in some situations to simply use USB2 for external USB storage. [OpenWRT](https://openwrt.org/docs/guide-user/network/wifi/usb3.0-wifi-issues) has a good article about this problem.
> Those USB3 cables can also cause interference for Bluetooth as it is on the 2.4 GHz band. I recommend users to not purchase USB WiFi adapters that contain both WiFi and Bluetooth as you are looking for problems. Buy separate adapters for Bluetooth and WiFi and use at least one extension cable to keep the devices away from each other. I have found it is best to get a USB2 extension cable for the USB Bluetooth adapter and to position the Bluetooth adapter away from USB3 cables and connections as well as away from active 2.4 GHz band WiFi devices.
> Another thing that I do when using 2.4 GHz WiFi is use a USB2 cable or USB2 L adapter to force my USB3 capable adapter to fallback to USB2 so as to reduce interference.
> Many people are unaware of the interference problems caused by USB3. It is best for you to understand this problem and take appropriate action. 
> Reference information from a White Paper from Intel dated 2012 (this is not a new issue): [Intel White Paper](https://www.usb.org/sites/default/files/327216.pdf)

### Summary

The Golden Rules to help you find USB WiFi Adapter(s) that meets your needs

- Research before buying. Ask questions in Issues.

  There are adapters of many sizes and capabilities.
  You need to define what capabilities and size you want before starting your search.
  Some questions to help you decide the capabilities and size you need:
  
  - Do you need long range?
  - Which channel bands do you need?
  - Which modes (e.g. managed, monitor, AP) need to be supported? 
  - Are there specific capabilities (e.g. active monitor mode) that need to be supported?

- Avoid multi-state adapters.

  As [previously noted](#windows-drivers), there are adapters that will first come up as flash drives or CDs so as to load a driver in Windows.
  This is an unnecessary feature that can cause problems even for Windows users.
  Who is going to update that Windows driver on the adapter as time passes?
  Nobody!

- Avoid multi-function adapters.

  Some USB WiFi adapters also have bluetooth capability.
  You do not want this!
  I have seen many problems with this over the years and bluetooth will likely limit the WiFi to USB2 speeds.
  If you need bluetooth capability, go get a seaparate bluetooth adapter or a M.2/PCIe card such as the ones based on the mt7922 or mt7925 chipsets.

- A good quality adapter can save you a lot of anguish.
  There are a lot of poor quality adapters on the market.

- Be careful when reading reviews.
  You often have to ignore what Windows users complain about. Reviews on single-state adapters, which is what we want, often have Windows users complaining about "why do I need to install a driver?" 

- Extension cables/stands and right angle usb adapters can greatly enhance the performance of your adapter.
  Use the shortest extension cable that will meet your needs.

- Avoid products by certain companies as they make things difficult for Linux users.
  See [the earlier explanation](#tp-link-and-d-link) in this document for details and avoid TP-Link products.

- Prefer adapters that are supported with Linux in-kernel drivers.
  [This document](./USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md) contains a LONG list of adapters and chipsets that are supported with in-kernel drivers.

- Be aware that USB3 cables and connections can interfere with 2.4 GHz WiFi and Bluetooth and work to mitigate resulting issues.

> [!TIP]
> If you are using a computer that has Secure Boot turned on and you want or need Secure Boot to stay on, please use USB WiFi adapters that use in-kernel drivers.
> A recommended list of proven adapters with in-kernel drivers is provided in [the Plug and Play List](./USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md).
> If you decide to use a Realtek chipset-based USB WiFi adapter that is only supported with out-of-kernel drivers, be prepared for a lot of challenges regarding Secure Boot.

![image](https://github.com/morrownr/USB-WiFi/assets/69053122/191306b2-f36c-4369-8944-de2bec784ba5)

-----

If there is additional information that you think would be helpful, please post in `Issues`.
