# Layout Management

A GUI widget can be placed inside the container window by specifying its absolute coordinates measured in pixels.

The coordinates are relative to the dimensions of the window defined by setGeometry() method.
  - ``QWidget.setGeometry(xpos, ypos, width, height)``

This Absolute Positioning, however, is not suitable because of following reasons:
  - The position of the widget does not change even if the window is resized.
  - The appearance may not be uniform on different display devices with different resolutions.
  - Modification in the layout is difficult as it may need redesigning the entire form.

PyQt API provides layout classes for more elegant management of positioning of widgets inside the container. The advantages of Layout managers over absolute positioning are:
  - Widgets inside the window are automatically resized.
  - Ensures uniform appearance on display devices with different resolutions.
  - Adding or removing widget dynamically is possible without having to redesign.

1. **QBoxLayout**
  - QBoxLayout class lines up the widgets vertically or horizontally.
  - ts derived classes are QVBoxLayout (for arranging widgets vertically) and QHBoxLayout (for arranging widgets horizontally).
2. **QGridLayout**
  - A GridLayout class object presents with a grid of cells arranged in rows and columns.
  - The class contains addWidget() method. Any widget can be added by specifying the number of rows and columns of the cell.
3. **QFormLayout**
  - QFormLayout is a convenient way to create two column form, where each row consists of an input field associated with a label.
  - As a convention, the left column contains the label and the right column contains an input field.
