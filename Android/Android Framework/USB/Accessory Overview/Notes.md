## Choose the right USB accessory APIs
Depending on what Android-powered devices you want to support, you might have to use one over the other:
1. com.android.future.usb 
    - To support USB accessory mode in Android 2.3.4
    - This add-on library is a thin wrapper around the android.hardware.usb accessory APIs and does not support USB host mode.
2. android.hardware.usb
    - This namespace contains the classes that support USB accessory mode in Android 3.1 and above.

## API Overview
The following table describes the classes that support the USB accessory APIs:
- **UsbManager:** Allows you to enumerate and communicate with connected USB accessories.
- **UsbAccessory:** Represents a USB accessory and contains methods to access its identifying information.

```kotlin
val manager = getSystemService(Context.USB_SERVICE) as UsbManager
val accessory = intent.getParcelableExtra(UsbManager.EXTRA_ACCESSORY) as UsbAccessory
```
## Android manifest requirements
- Because not all Android-powered devices are guaranteed to support the USB accessory APIs, include a <uses-feature> element that declares that your application uses the android.hardware.usb.accessory feature.
- If you are using the add-on library, add the <uses-library> element specifying com.android.future.usb.accessory for the library.
- Set the minimum SDK of the application to API Level 10 if you are using the add-on library or 12 if you are using the android.hardware.usb package.
- If you want your application to be notified of an attached USB accessory, specify an `<intent-filter>` and `<meta-data>` element pair for the android.hardware.usb.action.USB_ACCESSORY_ATTACHED intent in your main activity.
    - The <meta-data> element points to an external XML resource file that declares identifying information about the accessory that you want to detect.
- In the XML resource file, declare `<usb-accessory>` elements for the accessories that you want to filter.
    - Each <usb-accessory> can have the following attributes:
        - manufacturer
        - model
        - version

### Manifest file example
```xml
<manifest ...>
    <uses-feature android:name="android.hardware.usb.accessory" />
    
    <uses-sdk android:minSdkVersion="<version>" />
    ...
    <application>
      <uses-library android:name="com.android.future.usb.accessory" />
        <activity ...>
            ...
            <intent-filter>
                <action android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED" />
            </intent-filter>

            <meta-data android:name="android.hardware.usb.action.USB_ACCESSORY_ATTACHED"
                android:resource="@xml/accessory_filter" />
        </activity>
    </application>
</manifest>
```

### Resource file example
- Save the resource file in the res/xml/ directory.

```xml
<?xml version="1.0" encoding="utf-8"?>

<resources>
    <usb-accessory model="DemoKit" manufacturer="Google" version="1.0"/>
</resources>
```

## Work with accessories
When users connect USB accessories to an Android-powered device, the Android system can determine whether your application is interested in the connected accessory.

If so, you can set up communication with the accessory if desired. To do this, your application has to:
1. Discover connected accessories by using an intent filter that filters for accessory attached events or by enumerating connected accessories and finding the appropriate one.
2. Ask the user for permission to communicate with the accessory, if not already obtained.
3. Communicate with the accessory by reading and writing data on the appropriate interface endpoints.

### Descover an accessory using intent filter
To have your application discover a particular USB accessory, you can specify an intent filter to filter for the **android.hardware.usb.action.USB_ACCESSORY_ATTACHED** intent.

Along with this intent filter, you need to specify a resource file that specifies properties of the USB accessory, such as manufacturer, model, and version.

In your activity, you can obtain the UsbAccessory that represents the attached accessory from the intent like this:

```kotlin
val accessory = intent.getParcelableExtra(UsbManager.EXTRA_ACCESSORY) as UsbAccessory
```

### Obtain permission to communicate with an accessory
Before communicating with the USB accessory, your application must have permission from your users.

To explicitly obtain permission, first create a broadcast receiver. This receiver listens for the intent that gets broadcast when you call requestPermission().

The call to requestPermission() displays a dialog to the user asking for permission to connect to the accessory. 

> TODO

### Communicate with an accessory
You can communicate with the accessory by using the UsbManager to obtain a file descriptor that you can set up input and output streams to read and write data to descriptor.

You should set up the communication between the device and accessory in another thread, so you don't lock the main UI thread.

```kotlin
private lateinit var accessory: UsbAccessory
private var fileDescriptor: ParcelFileDescriptor? = null
private var inputStream: FileInputStream? = null
private var outputStream: FileOutputStream? = null
...

private fun openAccessory() {
    Log.d(TAG, "openAccessory: $mAccessory")
    fileDescriptor = usbManager.openAccessory(accessory)
    fileDescriptor?.fileDescriptor?.also { fd ->
        inputStream = FileInputStream(fd)
        outputStream = FileOutputStream(fd)
        val thread = Thread(null, this, "AccessoryThread")
        thread.start()
    }
}
```

In the thread's run() method, you can read and write to the accessory by using the FileInputStream or FileOutputStream objects.

When reading data from an accessory with a FileInputStream object, ensure that the buffer that you use is big enough to store the USB packet data.

### Terminate communication with an accessory
When you are done communicating with an accessory or if the accessory was detached, close the file descriptor that you opened by calling close().

To listen for detached events, create a broadcast receiver like below:

```kotlin
var usbReceiver: BroadcastReceiver = object : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {

        if (UsbManager.ACTION_USB_ACCESSORY_DETACHED == intent.action) {
            val accessory: UsbAccessory? = intent.getParcelableExtra(UsbManager.EXTRA_ACCESSORY)
            accessory?.apply {
                // call your method that cleans up and closes communication with the accessory
            }
        }
    }
}
```
