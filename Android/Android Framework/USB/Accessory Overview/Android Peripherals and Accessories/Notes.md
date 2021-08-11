Using a suite of standard protocols, you can implement compelling peripherals and other accessories that extend Android capabilities in a wide range of Android-powered devices.

An accessory for Android can be anything: keyboard, thermometer, robot, lighting control, or anything else you can imagine.

An accessory that connects to an Android device through a USB cable must support the **Android Open Accessory (AOA)** protocol, which specifies how an accessory can establish communication with an Android device via USB.
## Android Open Accessory (AOA)
Android Open Accessory (AOA) support allows external USB hardware (Android USB accessories) to interact with Android-powered devices in accessory mode.

Accessories should carry out the following steps:
1. Wait for and detect a connected device.
2. Determine the device's accessory mode support.
3. Attempt to start the device in accessory mode (if needed).
4. If the device supports AOA, establish communication with the device.

### Wait for and detect connected devices
Accessories should continuously check for connected Android-powered devices. When a device is connected, the accessory should determine if the device supports accessory mode.

### Determine accessory mode support
When an Android-powered device connects, it can be in one of three states:
- Supports Android accessory mode and is already in accessory mode.
- Supports Android accessory mode but it is not in accessory mode.
- Does not support Android accessory mode.

During the initial connection, the accessory should check the version, vendor ID, and product ID of the connected device's USB device descriptor.
- The vendor ID should match Google's ID (0x18D1).
- If the device is already in accessory mode, the product ID should be 0x2D00 or 0x2D01

The accessory can establish communication with the device through bulk transfer endpoints using its own communication protocol.

If the version, vendor ID, or product ID in the USB device descriptor do not match expected values, the accessory cannot determine if the device supports Android accessory mode.

### Attempt to start in accessory mode
1. Send a 51 control request ("Get Protocol") to determine if the device supports the Android accessory protocol.
- If the device supports the protocol, it returns a non-zero number that represents the supported protocol version.
2. If the device returns a supported protocol version, send a control request with identifying string information to the device.
- This information allows the device to determine an appropriate application for the accessory
3. Send a control request to ask the device to start in accessory mode.

After completing these steps, the accessory should wait for the connected USB device to re-introduce itself on the bus in accessory mode, then re-enumerate connected devices.

### Establish communication with the device
If the accessory detects an Android-powered device in accessory mode, the accessory can query the device interface and endpoint descriptors to obtain the bulk endpoints for communicating with the device.

