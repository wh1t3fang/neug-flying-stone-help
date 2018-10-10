# neug-flying-stone-help
When plugging the Neug Flying Stone TRNG into a Debian Linux machine it was detected as /dev/sdc because the device was in mass storage mode rather than USB CDC/ACM (Communication Device Class / Abstract Control Model) mode.  The following command worked:  

sudo eject /dev/sdc 

The device was now accesible on /dev/ttyACM0.  I could then use it to grab random data to wipe a hard drive like with the following command:

sudo dd if=/dev/ttyACM0 of=/dev/sdb 


In this example, the wiping process would be very slow as the device is not very fast.  However, you could use this in other applications such as mixing into /dev/urandom to provide additional entropy.  The following is my dmesg output to help others with diagnosis.  

[ 5788.410220] usb 3-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 5788.410223] usb 3-1: Product: Fraucheky
[ 5788.410225] usb 3-1: Manufacturer: Free Software Initiative of Japan
[ 5788.410227] usb 3-1: SerialNumber: FSIJ-0.0
[ 5788.412529] usb-storage 3-1:1.0: USB Mass Storage device detected
[ 5788.412757] scsi host7: usb-storage 3-1:1.0
[ 5789.424376] scsi 7:0:0:0: Direct-Access     FSIJ     Fraucheky        1.0  PQ: 0 ANSI: 0
[ 5789.466446] sd 7:0:0:0: Attached scsi generic sg1 type 0
[ 5789.485363] sd 7:0:0:0: [sdc] 128 512-byte logical blocks: (65.5 kB/64.0 KiB)
[ 5789.491345] sd 7:0:0:0: [sdc] Write Protect is off
[ 5789.491350] sd 7:0:0:0: [sdc] Mode Sense: 03 00 00 00
[ 5789.497199] sd 7:0:0:0: [sdc] No Caching mode page found
[ 5789.497206] sd 7:0:0:0: [sdc] Assuming drive cache: write through
[ 5789.538315]  sdc:
[ 5789.576428] sd 7:0:0:0: [sdc] Attached SCSI removable disk
[ 6004.837297] usb 3-1: USB disconnect, device number 11
[ 6004.846881] scsi 7:0:0:0: rejecting I/O to dead device
[ 6005.298904] usb 3-1: new full-speed USB device number 12 using ohci-pci
[ 6005.528113] usb 3-1: New USB device found, idVendor=234b, idProduct=0001, bcdDevice= 2.00
[ 6005.528117] usb 3-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 6005.528120] usb 3-1: Product: NeuG True RNG
[ 6005.528122] usb 3-1: Manufacturer: Free Software Initiative of Japan
[ 6005.528124] usb 3-1: SerialNumber: FSIJ-1.0.8-67255221
[ 6005.530608] cdc_acm 3-1:1.0: ttyACM0: USB ACM device

See this link for more info https://superuser.com/questions/899303/how-to-see-neug-fraucheky-true-random-number-generator  

