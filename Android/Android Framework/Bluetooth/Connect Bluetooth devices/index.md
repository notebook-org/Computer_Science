# Connect Bluetooth devices

To create a connection between two devices, you must implement both the **server-side** and **client-side** mechanisms because one device must open a server socket, and the other one must initiate the connection using the server device's MAC address.

The server device and the client device each obtain the required BluetoothSocket in different ways.
1. The server receives socket information when an incoming connection is accepted.
2. The client provides socket information when it opens an RFCOMM channel to the server.

The server and client are considered connected to each other when they each have a connected BluetoothSocket on the same RFCOMM channel.
    - At this point, each device can obtain input and output streams, and data transfer can begin.

## Connection techniques
1. Connect as a server
2. Connect as a client

### Connect as a client
In order to initiate a connection with a remote device that is accepting connections on an open server socket, you must first obtain a BluetoothDevice object that represents the remote device.

You must then use the BluetoothDevice to acquire a BluetoothSocket and initiate the connection.

1. Using the BluetoothDevice, get a BluetoothSocket by calling createRfcommSocketToServiceRecord(UUID)
2. Initiate the connection by calling connect(). Note that this method is a blocking call.
```kotlin
private inner class ConnectThread(device: BluetoothDevice) : Thread() {

   private val mmSocket: BluetoothSocket? by lazy(LazyThreadSafetyMode.NONE) {
       device.createRfcommSocketToServiceRecord(MY_UUID)
   }

   public override fun run() {
       // Cancel discovery because it otherwise slows down the connection.
       bluetoothAdapter?.cancelDiscovery()

       mmSocket?.let { socket ->
           // Connect to the remote device through the socket. This call blocks
           // until it succeeds or throws an exception.
           socket.connect()

           // The connection attempt succeeded. Perform work associated with
           // the connection in a separate thread.
           manageMyConnectedSocket(socket)
       }
   }

   // Closes the client socket and causes the thread to finish.
   fun cancel() {
       try {
           mmSocket?.close()
       } catch (e: IOException) {
           Log.e(TAG, "Could not close the client socket", e)
       }
   }
}
```
