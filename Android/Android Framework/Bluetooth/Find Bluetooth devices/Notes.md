Using the BluetoothAdapter, you can find remote Bluetooth devices either through **device discovery** or by **querying the list of paired devices**.

## Device discovery
It is a scanning procedure that searches the local area for Bluetooth-enabled devices and requests some information about each one.

Once a connection is made with a remote device for the first time, a pairing request is automatically presented to the user.

When a device is paired, the basic information about that device—such as the device's name, class, and MAC address—is saved and can be read using the Bluetooth APIs.

Note that there is a difference between being paired and being connected:
- To be paired means that two devices are aware of each other's existence, have a shared link-key that can be used for authentication, and are capable of establishing an encrypted connection with each other.
- To be connected means that the devices currently share an RFCOMM channel and are able to transmit data with each other.

## Query paired devices
Before performing device discovery, it's worth querying the set of paired devices to see if the desired device is already known.

To do so, call getBondedDevices().
- This returns a set of BluetoothDevice objects representing paired devices.
```kotlin
val pairedDevices: Set<BluetoothDevice>? = bluetoothAdapter?.bondedDevices
pairedDevices?.forEach { device ->
   val deviceName = device.name
   val deviceHardwareAddress = device.address // MAC address
}
```

To initiate a connection with a Bluetooth device, all that's needed from the associated BluetoothDevice object is the MAC address, which you retrieve by calling getAddress(). 
