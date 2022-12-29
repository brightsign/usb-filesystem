# usb-filesystem
Example using a BrightSign device as a filesystem over USB in Javascript.

## Overview

BrightSign players support USB role reversal modes through the USB-C ports on BrightSign players except for LS models. The BrightSign would be a USB client for an external device to utilize. The BrightSign can dynamically build a filesystem that is needed for the USB client to reference as the USB image.

This project provides an example for how to create a USB image file (.img) using built in BrightSign Javascript APIs, managing this filesystem file, and mounting or unmounting the filesystem as a mass storage device onto an external system. 

### System Requirements

- BrightSign OS 8.1.x
- BrightSign XD and XT Series 4

### Brightsign Javascript APIs

[@brightsign/filesysteminfile](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/404622545/filesysteminfile)

[@brightsign/usbfilesystem](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/404622824/usbfilesystem)


## Example BrightAuthor:connected Presentation

The example presentation and HTML file encompasses one approach for how you may send messages to HTML. The .html file is meant to highlight how to implement and utilize the filesystem and usb APIs. 

UDP commands are utilized throughout the sample presentation provided. The correct destination IP and port should be set in order for the Javascript app to receive the UDP commands sent from BrightAuthor:connected to the app. 

In the Presentation view under  “Presentation Settings” -> “Interactive” -> “Networking” -> “Specific IP Address” can be 127.0.0.1 and UDP Destination Port should be 5000. 


## BrightAuthor:connected  Integration

In BrightAuthor:connected, add the html / JavaScript file by adding an HTML Widget onto the interactive plane. From here, sending the UDPs mentioned below can be sent from anywhere in the presentation or from other Javascript processes to the destination IP and destination port. 

Command Parameter Structure
```
usb!!<command>!!<command parameter (optional)>
```

### Managing Filesystem

There are a couple commands which should be sent in order to allow for the app to understand how it should create the filesystem and the contents that are copied. 
___

_Command_: 
```
usb!!startfilesystem
```

_Description_: Sends a command to notify the app to acknowledge when to start listening to the addasset UDP commands below. 
___

_Command_: 
```
usb!!addasset!!<filename or directory>
```

_Description_: Sends a command to notify the app what is the name of a file or directory that should be copied to the usb drive. This command can be sent multiple times.

__Note__: The current expectation of this example is that the source dependencies live on the root of the SD card.
___

_Command_: 
```
usb!!closefilesystem
```

_Description_: Sends a command to notify the app to close and build the filesystem. The size for this example is 1GB, although this can be updated in the Javascript or additional support can be added to manage this at a more granular level using either “User Variables” or additional UDP commands.
___

### Mount filesystem

_Command_: 
```
usb!!mount
```

_Description_: Sends the command to mount the USB filesystem to the external client via the USB-C-to-USB-A cable.
___

### Unmount filesystem

_Command_: 
```
usb!!unmount
```

_Description_: Sends the command to unmount the USB filesystem to the external client via the USB-C-to-USB-A cable.
___