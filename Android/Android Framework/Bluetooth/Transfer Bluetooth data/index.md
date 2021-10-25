# Transfer Bluetooth data

After you have successfully connected to a Bluetooth device, each one has a connected BluetoothSocket. You can now share information between devices.

Using the BluetoothSocket, the general procedure to transfer data is as follows:
1. Get the InputStream and OutputStream that handle transmissions through the socket using getInputStream() and getOutputStream(), respectively.
2. Read and write data to the streams using read(byte[]) and write(byte[]).

```kotlin
private const val TAG = "MY_APP_DEBUG_TAG"

// Defines several constants used when transmitting messages between the
// service and the UI.
const val MESSAGE_READ: Int = 0
const val MESSAGE_WRITE: Int = 1
const val MESSAGE_TOAST: Int = 2
// ... (Add other message types here as needed.)

class MyBluetoothService(
       // handler that gets info from Bluetooth service
       private val handler: Handler) {

   private inner class ConnectedThread(private val mmSocket: BluetoothSocket) : Thread() {

       private val mmInStream: InputStream = mmSocket.inputStream
       private val mmOutStream: OutputStream = mmSocket.outputStream
       private val mmBuffer: ByteArray = ByteArray(1024) // mmBuffer store for the stream

       override fun run() {
           var numBytes: Int // bytes returned from read()

           // Keep listening to the InputStream until an exception occurs.
           while (true) {
               // Read from the InputStream.
               numBytes = try {
                   mmInStream.read(mmBuffer)
               } catch (e: IOException) {
                   Log.d(TAG, "Input stream was disconnected", e)
                   break
               }

               // Send the obtained bytes to the UI activity.
               val readMsg = handler.obtainMessage(
                       MESSAGE_READ, numBytes, -1,
                       mmBuffer)
               readMsg.sendToTarget()
           }
       }

       // Call this from the main activity to send data to the remote device.
       fun write(bytes: ByteArray) {
           try {
               mmOutStream.write(bytes)
           } catch (e: IOException) {
               Log.e(TAG, "Error occurred when sending data", e)

               // Send a failure message back to the activity.
               val writeErrorMsg = handler.obtainMessage(MESSAGE_TOAST)
               val bundle = Bundle().apply {
                   putString("toast", "Couldn't send data to the other device")
               }
               writeErrorMsg.data = bundle
               handler.sendMessage(writeErrorMsg)
               return
           }

           // Share the sent message with the UI activity.
           val writtenMsg = handler.obtainMessage(
                   MESSAGE_WRITE, -1, -1, mmBuffer)
           writtenMsg.sendToTarget()
       }

       // Call this method from the main activity to shut down the connection.
       fun cancel() {
           try {
               mmSocket.close()
           } catch (e: IOException) {
               Log.e(TAG, "Could not close the connect socket", e)
           }
       }
   }
}
```