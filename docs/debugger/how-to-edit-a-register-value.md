---
title: Edit a Register Value
description: Learn how to modify the contents of a register by editing its value in the Registers window (available only if address-level debugging is enabled).
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords: 
  - vs.debug.register.edit
dev_langs: 
  - C++
helpviewer_keywords: 
  - Registers window, editing register values
  - register values
author: mikejo5000
ms.author: mikejo
manager: mijacobs
ms.subservice: debug-diagnostics
---
# Edit a Register Value (C++)

The Registers window is available only if address-level debugging is enabled in the **Options** dialog box, **Debugging** node.

### To change the value of a register

1. In the **Registers** window, use the TAB key or the mouse to move the insertion point to the value you want to change. When you start to type, the cursor must be located in front of the value you want to overwrite.

2. Type the new value.

    > [!CAUTION]
    > Changing register values (especially in the EIP and EBP registers) can affect program execution.

    > [!CAUTION]
    > Editing floating-point values can result in minor inaccuracies because of decimal-to-binary conversion of fractional components. Even a seemingly innocuous edit can result in changes to some of the least significant bits in a floating-point register.

## Related content
- [How to: Use the Registers Window](../debugger/how-to-use-the-registers-window.md)
