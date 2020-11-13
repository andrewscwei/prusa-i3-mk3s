# Prusa i3 MK3S

This repo contains my Prusa i3 MK3S configurations.

## Resources

### Assembly

Follow the guide at https://help.prusa3d.com/en/category/original-prusa-i3-mk3s-kit-assembly_280.

### Firmware Upgrade

Download the firmware from https://www.prusa3d.com/drivers/ and follow the instructions [here](https://help.prusa3d.com/en/guide/upgrading-the-firmware-v1-6_24720).

### Replacing Printable Parts

Printable parts can be found here: https://www.prusa3d.com/prusa-i3-printable-parts/.

## Toshiba FlashAir W-04 Wi-Fi SD Card Setup (macOS)

Using the Toshiba FlashAir Wi-Fi cards allow you to a add/remove `.gcode` files to/from the SD card wirelessly without having to remove it physically. It's a convenient workaround to wireless printing for the Prusa i3 MK3S. Below are the steps to set up the card (note that the instructions are intended for the W-04 model, older models may or may not be compatible).

1. Make note of the master code of the SD card, which is the MAC address printed on the back of the card (12 alphanumeric characters).
2. Insert FlashAir SD card into your computer, ensure the card is unlocked.
3. Navigate to the root directory of the card and locate the file `SD_WLAN/CONFIG`. Open it and add/edit the following:
    1. Set the master code:
        ```ini
        MASTERCODE=<mac_address>
        ```
    2. Set the network settings:
       ```ini
       APPSSID=<network_ssid>
       APPNETWORKKEY=<network_password>
       ```
    3. The first line allows files to be uploaded to the card, the second line defines the default directory of uploaded files, and the third line indicates that the card can be mapped via WebDAV.
        ```ini
        UPLOAD=1
        UPDIR=/
        WEBDAV=2
        ```
    4. This turns the card to a client on your network rather than a standalone AP.
       ```ini
       APPMODE=5
       ```
    5. This sets the NetBIOS/Bonjour name of the card.
       ```ini
       APPNAME=<name>
       DHCP_Enabled=YES
       ```
4. Safely eject the card and insert it in the MK3S, navigate to **Settings**, scroll to **SD card**, and set it to `FlashAir`.
5. Connect to the card from Finder: **Go** > **Connect to Server...** > `http://<APPNAME>.local`, use any username and no password is needed.s

If all else fails, try reinitializing the SD card using the **FlashAir Configuration Software** downloaded from [here](http://www.toshiba-personalstorage.net/ww/support/download/flashair/w04/config.htm). The option can be accessed from the main menu > *Initialize the card/change settings* > *Initialize*.
