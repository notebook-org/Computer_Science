# USB host overview

When your Android-powered device is in USB host mode, it acts as the USB host, powers the bus, and enumerates connected USB devices.

## API Overview
| Class | Description |
| ----- | ----------- |
| **UsbManager** | Allows you to enumerate and communicate with connected USB devices. |
| **UsbDevice** | Represents a connected USB device and contains methods to access its identifying information, interfaces, and endpoints. |
| **UsbInterface** | Represents an interface of a USB device, which defines a set of functionality for the device. A device can have one or more interfaces on which to communicate. |
| **UsbEndpoint** | Represents an interface endpoint, which is a communication channel for this interface. An interface can have one or more endpoints, and usually has input and output endpoints for two-way communication with the device. |
| **UsbDeviceConnection** | Represents a connection to the device, which transfers data on endpoints. This class allows you to send data back and forth sychronously or asynchronously. |
| **UsbRequest** | Represents an asynchronous request to communicate with a device through a UsbDeviceConnection. |
| **UsbConstants** | Defines USB constants that correspond to definitions in linux/usb/ch9.h of the Linux kernel. |

## Android manifest requirements
The following list describes what you need to add to your application's manifest file before working with the USB host APIs:

- Because not all Android-powered devices are guaranteed to support the USB host APIs, include a <uses-feature> element that declares that your application uses the android.hardware.usb.host feature.
- Set the minimum SDK of the application to API Level 12 or higher. The USB host APIs are not present on earlier API levels.
- If you want your application to be notified of an attached USB device, specify an `<intent-filter>` and `<meta-data>` element pair for the android.hardware.usb.action.USB_DEVICE_ATTACHED intent in your main activity. 
    - The `<meta-data>` element points to an external XML resource file that declares identifying information about the device that you want to detect.

### Manifest and resource file example
```xml
<manifest ...>
    <uses-feature android:name="android.hardware.usb.host" />
    <uses-sdk android:minSdkVersion="12" />
    ...
    <application>
        <activity ...>
            ...
            <intent-filter>
                <action android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" />
            </intent-filter>

            <meta-data android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED"
                android:resource="@xml/device_filter" />
        </activity>
    </application>
</manifest>
```

Save the resource file in the res/xml/ directory.

```xml
<?xml version="1.0" encoding="utf-8"?>

<resources>
    <usb-device vendor-id="1234" product-id="5678" class="255" subclass="66" protocol="1" />
</resources>
```

## Work with devices
When users connect USB devices to an Android-powered device, the Android system can determine whether your application is interested in the connected device.

If so, you can set up communication with the device if desired. To do this, your application has to:
1. Discover connected USB devices by using an intent filter to be notified when the user connects a USB device or by enumerating USB devices that are already connected.
2. Ask the user for permission to connect to the USB device, if not already obtained.
3. Communicate with the USB device by reading and writing data on the appropriate interface endpoints.
