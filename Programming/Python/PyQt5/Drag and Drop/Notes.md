The provision of drag and drop is very intuitive for the user.
  - It is found in many desktop applications where the user can copy or move objects from one window to another.

MIME based drag and drop data transfer is based on **QDrag** class.

**QMimeData** objects associate the data with their corresponding MIME type.
  - It is stored on clipboard and then used in the drag and drop process.

MIME Types: text/plain, text/html, text/uri-list, image/ *, application/x-color

Many QWidget objects support the drag and drop activity.
  - Those that allow their data to be dragged have setDragEnabled() which must be set to true.

On the other hand, the widgets should respond to the drag and drop events in order to store the data dragged into them.
  - **DragEnterEvent** provides an event which is sent to the target widget as dragging action enters it.
  - **DragMoveEvent** is used when the drag and drop action is in progress.
  - **DragLeaveEvent** is generated as the drag and drop action leaves the widget.
  - **DropEvent**, on the other hand, occurs when the drop is completed. The event’s proposed action can be accepted or rejected conditionally.
