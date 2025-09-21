## USB-WiFi Frequently Asked Questions (FAQ)

Note: If you find that any of the answers below no longer work or are in need of an update, please let me know by posting a message in `issues`. Keeping the information on this site current is a challenge and can only work with your help. Thanks.

No. 1 - Question: It appears that the Wireless Regulatory information is not correct in my system. How can I fix this?

No. 2 - Question: My 6 GHz band shows as disabled when I run `iw list`. I want to be
able to use the 6 GHz band. How can I fix this?

No. 3 - Question: Why do I see high levels of jitter with my mt7922 or mt7921 based wifi card (PCIe or M.2)?

No. 4 - Question: Why do I see high levels of jitter with my USB WiFi adapter?

No. 5 - Question: I am having problems with my Alfa AXML or Alfa AXM. The wifi is not working. It seems to crash when coming up. What can I do?

No. 6 - Question: I live in the US and am trying to use a tri-band USB WiFi adapter as an AP with band 4 (6 GHz). How do I make it work?

No. 7 - Question: My USB WiFi adapter is showing up as a CDROM or Flash drive instead of a WiFi adapter. What is the problem?

-----

No. 1

Question: It appears that the Wireless Regulatory information is not correct in my system. How can I fix this?

Know the Country Code for your Country: [List of Current ISO 3166 country codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) ( Example: Panama = PA )

For reference: Official Linux Wireless documentation: [Linux Wireless documentation](https://wireless.docs.kernel.org/en/latest/index.html)

Information: When you run `iw reg get` you should be able to see the country code setting of your system and the information about the bands that you can use. Here is an example of what you should see. My country is US, so I see the following:

```
$ iw reg get
global
country US: DFS-FCC
	(902 - 904 @ 2), (N/A, 30), (N/A)
	(904 - 920 @ 16), (N/A, 30), (N/A)
	(920 - 928 @ 8), (N/A, 30), (N/A)
	(2400 - 2472 @ 40), (N/A, 30), (N/A)
	(5150 - 5250 @ 80), (N/A, 23), (N/A), AUTO-BW
	(5250 - 5350 @ 80), (N/A, 24), (0 ms), DFS, AUTO-BW
	(5470 - 5730 @ 160), (N/A, 24), (0 ms), DFS
	(5730 - 5850 @ 80), (N/A, 30), (N/A), AUTO-BW
	(5850 - 5895 @ 40), (N/A, 27), (N/A), NO-OUTDOOR, AUTO-BW, PASSIVE-SCAN
	(5925 - 7125 @ 320), (N/A, 12), (N/A), NO-OUTDOOR, PASSIVE-SCAN
	(57240 - 71000 @ 2160), (N/A, 40), (N/A)


```

Note: If you are located in another country, the 2 letter country code should reflect your country code.

Example of what you may see if there is no country code set and your system is having to use the global defaults:

```
$ sudo iw reg get
global
country 00: DFS-UNSET
	(2402 - 2472 @ 40), (6, 20), (N/A)
	(2457 - 2482 @ 20), (6, 20), (N/A), AUTO-BW, PASSIVE-SCAN
	(2474 - 2494 @ 20), (6, 20), (N/A), NO-OFDM, PASSIVE-SCAN
	(5170 - 5250 @ 80), (6, 20), (N/A), AUTO-BW, PASSIVE-SCAN
	(5250 - 5330 @ 80), (6, 20), (0 ms), DFS, AUTO-BW, PASSIVE-SCAN
	(5490 - 5730 @ 160), (6, 20), (0 ms), DFS, PASSIVE-SCAN
	(5735 - 5835 @ 80), (6, 20), (N/A), PASSIVE-SCAN
	(57240 - 63720 @ 2160), (N/A, 0), (N/A)


```

Notice that `country 00: DFS-UNSET` indicates no country code is set.

What are some of the results of the country code not being set?

- 5 GHz channels do not allow access point operation (i.e. `iw list` shows No-IR on all channels).
- Some 5 GHz channels that should be available are not available.
- 6 GHz channels completely disabled.
- 2.4 GHz channel may show a lower txpower than what is allowed in your country.

The list above is only a partial list of problems that can arise if the country code is not set properly.

The first step to fix this problem is to try to set the Country Code manually:

Open a Terminal interface - Ctrl + Alt + T

```
sudo iw reg set AU
```

Check to see if this fixes the problem:

```
iw reg get
```

If the Country Code is now set, I recommend that you skip to Answer 2 below to make the setting persistent. If the Country Code is not set, then I recommend trying Answer 1.

Answer 1:

If you are using Arch Linux or distros that are based on Arch Linux first follow the following section, otherwise skip it:

```
Setting the Wireless Regulatory Domain in Arch Linux

Install wireless-regdb:

If you haven't already, install the wireless-regdb package: sudo pacman -S wireless-regdb

Edit /etc/conf.d/wireless-regdom

```

Open the file with a text editor and uncomment the line containing your desired regulatory
domain. For example, to set it to the United States, you might uncomment REGDOMAIN="US". 

Save the file

Reboot:

```
sudo reboot
```

To check if the country code setting of your system is now correct:

```
iw reg get

```

If you are NOT using Arch Linux or distros that are based on Arch Linux

Open a Terminal interface - Ctrl + Alt + T

Create the following file:

```
sudo nano /etc/modprobe.d/cfg80211.conf

```

Note: You can use your own favorite text editor in place of `nano` if you wish.

Add the following line to the file:

```
options cfg80211 ieee80211_regdom=AU

```

Note: If your country code is not AU, you will need to replace AU with your country code

Save the file: (if using `nano`)

```
Ctrl + O, Enter, Ctrl + X

```

Reboot:

```
sudo reboot
```

To check if the country code setting of your system is now correct:

```
iw reg get

```

Answer 2:

Open a Terminal interface - Ctrl + Alt + T

Create the following file:

```
sudo nano /etc/systemd/system/regdom.service

```

Note: You can use your own favorite text editor in place of `nano` if you wish.

Add the following lines to the file:

```
[Unit]
Description=Set wireless regulatory domain to US

[Service]
ExecStart=/usr/sbin/iw reg set US

[Install]
WantedBy=multi-user.target

```

Note: If your country code is not US, you will need to replace US with your country code

Save the file: (if using `nano`)

```
Ctrl + O, Enter, Ctrl + X

```

Run the following command to activate the new service file:

```
sudo systemctl enable regdom.service

```

Reboot:

```
sudo reboot

```

After reboot it should have run the command. You can check with:

```
systemctl status regdom

```

To check if the country code setting of your system is now correct:

```
iw reg get

```


-----


No. 2

Question: My 6 GHz band shows as disabled when I run `iw list`. I want to be
able to use the 6 GHz band. How can I fix this?

Answer:  This may happen with MEDIATEK cards and adapters on Linux 6.7.x or
newer. There has been a lot of work on the WiFi support in Linux over the
last year. We have seen an uptick in WiFi problems as a result. As of kernel
6.12, things seem to be getting better but there is work to be done.

A new feature called "CLC (Country Location Control)" must be disabled in the
`mt7921_common` module in order to use the 6 GHz band (for now). Make a file
called `/etc/modprobe.d/mt7921.conf` containing `options mt7921_common disable_clc=1`.

Example:

Open a Terminal interface - Ctrl + Alt + T

Create the following file:

```
sudo nano /etc/modprobe.d/mt7921.conf

```

Note: You can use your own favorite text editor in place of `nano` if you wish.

Add the following line to the file:

```
options mt7921_common disable_clc=1

```

Save the file: Ctrl + O, Enter, Ctrl + X

Reboot:

```
sudo reboot

```

Source: https://community.frame.work/t/responded-amd-rz616-wifi-card-doesnt-work-with-6ghz-on-kernel-6-7/43226

Information: https://bugzilla.kernel.org/show_bug.cgi?id=218731

-----


No. 3

Question: Why do I see high levels of jitter with my mt7922 or mt7921 based wifi card (PCIe or M.2)?

Information: Variance in ping times is called "jitter" in networking terminology; it refers to the inconsistency in the arrival time of data packets, essentially measuring how much your ping fluctuates over time. Jitter disrupts the smooth flow of data, resulting in noticeable disruptions, particularly in time-sensitive activities. 

Information: Both chips use the mt7921e driver.

Answer: You can try disabling power management for that card as follows:

Open a Terminal interface - Ctrl + Alt + T

Create the following file:

```
sudo nano /etc/modprobe.d/mt7921.conf

```

Note: You can use your own favorite text editor in place of `nano` if you wish.

Add the following line to the file:

```
options mt7921e disable_aspm=Y

```

Save the file: Ctrl + O, Enter, Ctrl + X

Reboot:

```
sudo reboot

```


-----


No. 4

Question: Why do I see high levels of jitter with my USB WiFi adapter?

Information: Variance in ping times is called "jitter" in networking terminology; it refers to the inconsistency in the arrival time of data packets, essentially measuring how much your ping fluctuates over time. Jitter disrupts the smooth flow of data, resulting in noticeable disruptions, particularly in time-sensitive activities.

Important: Jitter can often be caused by or increased greatly by `low signal level` so I always check `signal level` before trying anything else. A signal level greater than `-52 dBm` may be at a level that can adversely affect jitter levels. Examples of signal levels greater than`-52 dBm` would be `-53 dBm, -54 dBm, -55 dBm, etc.` You may need to take action to lower the signal level reading (that is, increase the signal strength). Placement of the wireless devices can often contribute to poor signal strength. If you have investigated signal strength and are still seeing less than optimal results, see below.


Answer 1: First test to see if power_save is causing the issue:

Open a Terminal interface: Ctrl + Alt + T

Run the following command (remember to change wlan0 to the name of your wireless interface):

```
iw wlan0 set power_save off
```

Do not reboot as that will return power_save to on.

Test your system to see if there is improvement. If there is improvement, you may want to check the additional answers below for a persistent solution.


Answer 2: If your system uses `Network Manager`, you can disable power_save for the adapter as follows:

Open a Terminal interface: Ctrl + Alt + T

Create the following file:

```
sudo nano /etc/NetworkManager/conf.d/wifi-power_save.conf
```

Note: You can use your own favorite text editor in place of `nano` if you wish.

Add the following lines to the file:

```
# Values are 0 (use default), 1 (ignore/don't touch), 2 (disable) or 3 (enable).
wifi.powersave = 2
```

Save the file: Ctrl + O, Enter, Ctrl + X

Reboot:

```
sudo reboot
```


Answer 3:

If your system uses `systemd`, you can disable power_save for the adapter as follows:

Open a Terminal interface: Ctrl + Alt + T

Create the following file:

Note: You can use your own favorite text editor in place of `nano` if you wish.

```
sudo nano /lib/systemd/system/wifi-power_save.service
```

Add the following lines to the file (remember to change `wlan0` to the name of your wireless interface):

```
[Unit]
Description=Disable power_save for specific USB WiFi adapter
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/iw wlan0 set power_save off

[Install]
WantedBy=default.target
```

Save the file: Ctrl + O, Enter, Ctrl + X

Run the following command to enable the new service:

```
sudo systemctl enable wifi-power_save.service
```

Run the following command to verify that the service is functioning properly after rebooting:

Note: remember to change `wlan0` to the name of your wireless interface.

```
iw wlan0 get power_save
```

Run the following command to disable the service if you need to disable it:

```
sudo systemctl disable wifi-power_save.service
```


-----


No. 5

Question: I am having problems with my Alfa AXML or Alfa AXM. The wifi is not working. It seems to crash when coming up. What can I do?

Update as of the release of Ubuntu 25.04: Both adapters are working fine with the 25.04 release of Ubuntu which uses kernel 6.14 and the most up to date firmware files. WiFi and Bluetooth both work. It was a bluetooth related bug that was preventing wifi from working.

Answer: This was a known problem that started in 2024 after the release of kernel 6.7. There were unsuccessful attempts to fix this problem but a fix was finally found in late 2024 and worked it way into kernel 6.14. It was a strange problem in that bluetooth was involved. Most adapters with the mt7921au chipset do not have this problem because bluetooth is not active. The adapters listed in the question are the only ones known to have bluetooth active so this problem only showed up on the Alfa AXML and AXM. If you are using a kernel that has not been patched, a workaround is to disable bluetooth. The simplest way to disable the bluetooth support for these adapters is to delete the firmware file for bluetooth support for the mt7921au chip:

sudo rm /lib/firmware/mediatek/BT_RAM_CODE_MT7961_1_2_hdr.bin

-----

You may also want to ensure you are running the latest firmware files for the mt7921au chipset

Make sure you're running the latest WiFi firmware:

As of 2025/05/06, the most up to date firmware files:

[18615.766176] mt7921u 1-9.3:1.3: WM Firmware Version: ____010000, Build Time: 20241106151045

Instructions for updating the firmware can be found at the following location:

https://github.com/morrownr/USB-WiFi/blob/main/home/How_to_Install_Firmware_for_Mediatek_based_USB_WiFi_adapters.md

-----

If WiFi is not working in a USB3 port, try a USB2 port or a USB2 hub.

-----

The above solution, that shuts down bluetooth support, may not work
well for people that have other bluetooth support in their system and
they want to use it. In that case, simply delete BT firmware file for
your adapter.

-----

No. 6

Question: I live in the US and am trying to use a tri-band USB WiFi adapter as an AP with band 4 (6 GHz). How do I make it work?


Answer: This capability works in many locations in the world such as the EU countries. It is currently problematic in the US due to US wireless regulations. This is true of USB WiFi adapters with Mediatek and Realtek chips as the issue is not with the hardware or drivers. The problem is with US wireless regulations as shown in db.txt (I'll add more information on how to research this as I have time.) Here is a link that explains the problem:

https://patchwork.kernel.org/project/linux-wireless/patch/000201db8822$98f28da0$cad7a8e0$@gmail.com/


-----

No. 7

Question: My USB WiFi adapter is showing up as a CDROM or Flash drive instead of a WiFi adapter. What is the problem?

Answer: Your USB WiFi adapter showing up as a CDROM or Flash drive (often with ID 0bda:1a2b) instead of functioning as a network adapter (such as ID 35bc:0102 or similar) is likely due to a "mode-switching" issue. Some USB WiFi adapters include onboard memory that contains drivers or installation software for Windows. When plugged into a system for the first time, they initially present themselves as a virtual CD-ROM or Flash driver containing the drivers. This is fairly common with USB WiFi adapters that use Realtek chipset.

In Linux, the `usb_modeswitch` utility generally handles this issue but there are situations where it does not work as expected.

Your options:

Option 1: Send your adapter back and get one that is single-state (no storage onboard). If that is not possible then:

Option 2: You need to check if the VID/PID for your adapter is in the usb_modeswitch data file. See the following link for more information:

https://github.com/morrownr/USB-WiFi/blob/main/home/How_to_Modeswitch.md

Option 3: If you have exhausted recommendations from the information in item 2, then:

You may be able to make the adapter work in wifi mode with the following method:

How to add kernel parameters with GRUB in Ubuntu:

Note: This method may vary by distro so if you are not using Ubuntu, please consult the documentation for your distro.

Once your device has booted, use a text editor to open the following file:

```
$ sudo nano /etc/default/grub
```

Add parameters to `GRUB_CMDLINE_LINUX` while keeping the following in mind:

Enter parameters inside the double-quotes

Leave a space before each new parameter

Don’t add space round = and other punctuations for each key-value

Don’t add line breaks

If your original line looks like:

GRUB_CMDLINE_LINUX="quiet"

Then your updated line should read like:

GRUB_CMDLINE_LINUX="quiet usb-storage.quirks=0bda:1a2b:i"

Note: If the storage VID/PID (ID) is not 0bda:1a2b, you will need to change 0bda:1a2b to the storage mode VID/PID of your adapter.

Save and close the editor.

Update GRUB with its new configuration:

```
$ sudo update-grub
```

```
$ sudo reboot
```

Note: If your distro does not use grub, the RasPiOS is an example, you will need to read your distro docs to see how to do the above.

Example for Raspberry Pi OS:

```
$ sudo nano /boot/firmware/cmdline.txt
```

add the following to the end of the console= line:

usb-storage.quirks=0bda:1a2b:i

Save, close the editor and reboot.

-----

No. 8

Question: It appears that I cannot the change or accurately check the txpower of my USB WiFi adapter. How can I fix this?

NOTICE: This FAQ item is a WORK IN PROGRESS. You are welcome to help.

Answer:

rtw88 ignores the txpower command from iw, no matter what chip you are using.

Is the above statement true for rtw89 and mt76?

The following is captured from https://github.com/lwfinger/rtw88/issues/111 and is being used as a starting point.

The SAR thing is this command from iw:
```
iw phy <phyname> set sar_specs <sar type> <range index:sar power>*
```

sar type can be only 0 (NL80211_SAR_TYPE_POWER) right now.

range index is 0, 1, 2, or 3, depending on which frequency range you are working with:

```
[0] = { .start_freq = 2412, .end_freq = 2484, },
[1] = { .start_freq = 5180, .end_freq = 5320, },
[2] = { .start_freq = 5500, .end_freq = 5720, },
[3] = { .start_freq = 5745, .end_freq = 5825, },
```

And sar power is in units of 0.25 dBm.

You can see the effect of the command via debugfs:

```
# head /sys/kernel/debug/ieee80211/phy1/rtw88/tx_pwr_tbl

channel: 106                                                                                                                                                               
bandwidth: 2                                                                                                                                                               
regulatory: ETSI                                                                                                                                                           
path rate       pwr       base      (byr  lmt  sar ) rem                                                                                                                   
   A  OFDM_6M    26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  
   A  OFDM_9M    26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  
   A  OFDM_12M   26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  
   A  OFDM_18M   26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  
   A  OFDM_24M   26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  
   A  OFDM_36M   26(0x1a)   24    2 (   4    2   63)    0                                                                                                                  

# iw phy1 set sar_specs 0 2:50

# head /sys/kernel/debug/ieee80211/phy1/rtw88/tx_pwr_tbl

channel: 106
bandwidth: 2
regulatory: ETSI
path rate       pwr       base      (byr  lmt  sar ) rem 
   A  OFDM_6M    19(0x13)   24   -5 (   4    2   -5)    0
   A  OFDM_9M    19(0x13)   24   -5 (   4    2   -5)    0
   A  OFDM_12M   19(0x13)   24   -5 (   4    2   -5)    0
   A  OFDM_18M   19(0x13)   24   -5 (   4    2   -5)    0
   A  OFDM_24M   19(0x13)   24   -5 (   4    2   -5)    0
   A  OFDM_36M   19(0x13)   24   -5 (   4    2   -5)    0
```



Not sure if the following has anything to do with this issue but here it is for now.

For Wi-Fi power regulations, the kernel's cfg80211 subsystem defines SAR (Spectral Activity Regulation) capabilities and configurations through structures like ieee80211_iface_combination and nl80211_put_sar_specs. 

System Activity Monitoring with `sar`

The sar command is part of the sysstat package and is used for monitoring system resource usage, including network activity.

Installation on Debian 13:

```
sudo apt install sysstat; on Ubuntu, edit /etc/default/sysstat to enable it. 
```

Enable `sysstat`:

```
sudo nano /etc/default/sysstat
```

Change the following line:

ENABLED="false"

to:

ENABLED="true"

-----
