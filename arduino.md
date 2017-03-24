# Can't open device 'COM'

> Enter this in console ONCE

```console
> $ sudo usermod -a -G dialout <username>
```

> Type it in **console**

```console
$ sudo usermod -a -G dialout rozmathplus
```

> And this 

```console
> $ sudo chmod a+rw /dev/ttyACM<**number**>
```

> Type it in **console**

```console
$ sudo chmod a+rw /dev/ttyACM0
```





# WIRELESS DEBUGGING APC'S

https://developer.android.com/studio/command-line/adb.html#wireless

> Connect your Android device and adb host computer to a common Wi-Fi network accessible to both. Beware that not all access points are suitable; you might need to use an access point whose firewall is configured properly to support adb.
If you are connecting to an Android Wear device, turn off Bluetooth on the phone that's paired with the device.
Connect the device to the host computer with a USB cable.
Set the target device to listen for a TCP/IP connection on port 5555.

```console
adb tcpip 5555
```

> Disconnect the USB cable from the target device.
Find the IP address of the Android device. For example, on a Nexus device, you can find the IP address at Settings > About tablet (or About phone) > Status > IP address. Or, on an Android Wear device, you can find the IP address at Settings > Wi-Fi Settings > Advanced > IP address.
Connect to the device by its IP address.

```console
adb connect **device_ip_address**
```

> Confirm that your host computer is connected to the target device:

```console
$ adb devices

\> List of devices attached
**device_ip_address**:5555 **device**
```
