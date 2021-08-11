To use Bluetooth features in your app, you must declare two permissions:
1. **BLUETOOTH** is necessary to perform any Bluetooth communication, such as requesting a connection, accepting a connection, and transferring data.
2. **ACCESS_FINE_LOCATION** is necessary because a Bluetooth scan can gather information about the location of the user.

If you want your app to initiate device discovery or manipulate Bluetooth settings, you must declare the BLUETOOTH_ADMIN permission in addition to the BLUETOOTH permission.

```xml
<manifest ... >
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<!-- If your app targets Android 9 or lower, you can declare
     ACCESS_COARSE_LOCATION instead. -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
     ...
</manifest>
```
