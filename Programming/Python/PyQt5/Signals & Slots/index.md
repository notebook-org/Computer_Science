# Signals & Slots

Unlike a console mode application, which is executed in a sequential manner, a GUI based application is event driven.
  -  Functions or methods are executed in response to user’s actions like clicking on a button, selecting an item from a collection or a mouse click etc., called events.

Widgets used to build the GUI interface act as the source of such events.

Each PyQt widget, which is derived from QObject class, is designed to emit **signal** in response to one or more events.

The signal on its own does not perform any action. Instead, it is connected to a **slot**.
  - The slot can be any callable Python function.

## Building Signal-Slot Connection
You can establish signal-slot connection by following syntax:
```
widget.signal.connect(slot_function)
```
