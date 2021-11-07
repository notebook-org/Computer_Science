A typical GUI application may have multiple windows.
  - Tabbed and stacked widgets allow to activate one such window at a time.
  - However, many a times this approach may not be useful as view of other windows is hidden.

One way to display multiple windows simultaneously is to create them as independent windows.
  - This is called as **SDI (single Document Interface)**.
  - This requires more memory resources as each window may have its own menu system, toolbar, etc.

**MDI (Multiple Document Interface)** applications consume lesser memory resources.
  - The sub windows are laid down inside main container with relation to each other.
  - The container widget is called **QMdiArea**.

**QMdiArea** widget generally occupies the central widget of **QMainWindow** object.
  - Child windows in this area are instances of **QMdiSubWindow** class.
  - It is possible to set any QWidget as the internal widget of subWindow object.
  - Sub-windows in the MDI area can be arranged in cascaded or tile fashion.
