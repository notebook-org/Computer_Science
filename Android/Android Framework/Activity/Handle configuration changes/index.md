# Handle configuration changes

## References
* [Docs Link](https://developer.android.com/guide/topics/resources/runtime-changes)

# Handle configuration changes
- Some device configurations can change during runtime
  - such as screen orientation.
- When such a change occurs, Android restarts the running Activity.
  - onDestroy() is called, followed by onCreate()
- The restart behavior is designed to help your application adapt to new configurations by automatically reloading your application with alternative resources that match the new device configuration.
- To properly handle a restart, it is important that your activity restores its previous state.
  - You can use a combination of onSaveInstanceState(), ViewModel objects, and persistent storage to save and restore the UI state of your activity across configuration changes.
  - For more details reffer [Saving UI States](https://developer.android.com/topic/libraries/architecture/saving-states).
- You might encounter a situation in which restarting your application and restoring significant amounts of data can be costly and create a poor user experience. In such a situation, you have two other options:
  1. Retain an object during a configuration change
  2. Handle the configuration change yourself
    - It is not recommended to handle configuration changes yourself due to the hidden complexity of handling the configuration changes.
