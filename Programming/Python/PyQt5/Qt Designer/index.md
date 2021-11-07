# Qt Designer

It is a GUI tool to build GUI by drag and drop.

The ui is saved in **\*.ui file**

This design is translated into Python equivalent by using pyuic5 command line utility.
  - Example: ``pyuic5 -x demo.ui -o demo.py``
  - In the above command, -x switch adds a small amount of additional code to the generated Python script (from XML) so that it becomes a self-executable standalone application.


