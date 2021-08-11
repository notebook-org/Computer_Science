# Set up Bluetooth

Before your app can communicate over Bluetooth, you need to verify that Bluetooth is supported on the device, and if it is, ensure that it is enabled.
    - Note that this check is only necessary if the android:required attribute in the `<uses-feature.../>` manifest file entry is set to false.

If Bluetooth is supported, but disabled, then you can request that the user enable Bluetooth without leaving your app.

The first step is adding the Bluetooth permissions to your manifest file in order to use the following APIs.

Once the permissions are in place, Bluetooth setup is accomplished in two steps using the BluetoothAdapter:
1. Get the **BluetoothAdapter**.
    - The BluetoothAdapter is required for any and all Bluetooth activity.
    - There's one Bluetooth adapter for the entire system, and your app can interact with it using this object.
    - To get the BluetoothAdapter, call the static getDefaultAdapter() method. If getDefaultAdapter() returns null, then the device doesn't support Bluetooth.
    ```kotlin
    val bluetoothAdapter: BluetoothAdapter? = BluetoothAdapter.getDefaultAdapter()
    if (bluetoothAdapter == null) {
      // Device doesn't support Bluetooth
      }
    ```
2. Enable Bluetooth. 
    - Next, you need to ensure that Bluetooth is enabled.
        - Call isEnabled() to check whether Bluetooth is currently enabled.
    - To request that Bluetooth be enabled, call startActivityForResult(), passing in an ACTION_REQUEST_ENABLE intent action.
        - This call issues a request to enable Bluetooth through the system settings
        ```kotlin
        if (bluetoothAdapter?.isEnabled == false) {
          val enableBtIntent = Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE)
            startActivityForResult(enableBtIntent, REQUEST_ENABLE_BT)
            }
        ```
    - A dialog appears requesting user permission to enable Bluetooth.
    - Your app can also listen for the ACTION_STATE_CHANGED broadcast intent, which the system broadcasts whenever the Bluetooth state changes.
