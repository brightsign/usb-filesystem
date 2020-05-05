# usb-filesystem
example of using a brightsign device as a filesystem over USB

1. Overview

BrightSign players support USB role reversal modes through the USB-C ports on BrightSign players. The BrightSign would be a USB client for an external device to utilize. The BrightSign can dynamically build a filesystem that is needed for the USB client to reference as the USB image. If needed, please ask BrightSign for an example presentation that demonstrates how to utilize the commands outlined below. 

Note: If a presentation has been provided, this is to be used as an example when integrating projects with USB or Filesystem objects in Brightscript or Javascript.

Support:

BrightSign OS 8.1.x

BrightSign XD and XT Series 4

1.1. Scope

Documentation on the usage for Brightsign Javascript APIs:

@brightsign/filesysteminfile

@brightsign/usbfilesystem


2. Instructions

2.1. Updating USB Filesystem

UDP commands are utilized throughout the sample presentation provided. The correct destination IP and port should be set in order for the Javascript app to receive the UDP commands sent from BrightAuthor:connected to the app. 

In the Presentation view under  “Presentation Settings” -> “Interactive” -> “Networking” -> “Specific IP Address” can be 127.0.0.1 and UDP Destination Port should be 5000. 

2.2. BrightAuthor Integration

In BrightAuthor:connected, add the html / JavaScript file by adding an HTML Widget onto the interactive plane. From here, sending the UDPs mentioned below can be sent from anywhere in the presentation or from other Javascript to the destination IP and destination port. 

Command Parameter Structure: usb!<command>!<command parameter (optional)>

2.3. Managing Filesystem

There are a couple commands which should be sent in order to allow for the app to understand how it should create the filesystem and the contents that are copied. 

Command: usb!startfilesystem

Description: Sends a command to notify the app to acknowledge when to start listening to the addasset UDP commands below. 

Command: usb!addasset!<filename or directory>
  
Description: Sends a command to notify the app what is the name of a file or directory that should be copied to the usb drive. This command can be sent multiple times.

Note: The current expectation of this example is that the source dependencies live on the root of the SD card.

Command: usb!closefilesystem

Description: Sends a command to notify the app to close and build the filesystem. The size for this example is 1GB, although this can be updated in the Javascript or additional support can be added to manage this at a more granular level using either “User Variables” or additional UDP commands.

2.4. Mount/Unmount filesystem

2.4.1. Mount

Command: usb!mount

Description: Sends the command to mount the USB filesystem to the external client via the USB-C-to-USB-A cable.

2.4.2. Unmount

Command: usb!unmount

Description: Sends the command to unmount the USB filesystem to the external client via the USB-C-to-USB-A cable.
