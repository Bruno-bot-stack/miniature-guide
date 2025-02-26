---
title: Toggle word wrap to see long code or line numbers
description: Enable word wrapping in Visual Studio so long lines of code display on multiple lines in the Code Editor, or turn the feature off to see line numbers.
ms.date: 04/06/2023
ms.topic: how-to
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
author: anandmeg
ms.author: meghaanand
manager: mijacobs
ms.subservice: general-ide
---
# Manage word wrap in the editor

You can set and clear the **Word wrap** option. When this option is set, the portion of a long line that extends beyond the current width of the Code Editor window is displayed on the next line. When this option is cleared&mdash;for example, to facilitate the use of line numbering&mdash;you can scroll to the right to see the ends of long lines.

> [!NOTE]
> This topic applies to Visual Studio on Windows. For Visual Studio for Mac, see [Source editor: Word wrap](/visualstudio/mac/source-editor#word-wrap).

## To set word wrap preferences

1. On the Visual Studio menu bar, select **Tools** > **Options**.

    :::image type="content" source="media/vs-2022/tools-options-menu-bar.png" alt-text="Screenshot of the menu bar in Visual Studio with Tools and Options selected.":::

1. Select **Text Editor** > **All Languages** > **General** to set this option globally.

     — or —

     Select **Text Editor**, select the folder that matches the programming language you're using, and then select the **General** folder. For example, select **Text Editor** > **C#** > **General**.

1. Under **Settings**, select or clear the **Word wrap** option.

     When the **Word wrap** option is selected, the **Show visual glyphs for word wrap** option is enabled.

    > [!NOTE]
    > The **Show visual glyphs for Word Wrap** option displays a return-arrow indicator where a long line wraps onto a second line. These reminder arrows are not added to your code; they are for display purposes only.

## Known issues

If you're familiar with word wrap in Notepad++, Sublime Text, or Visual Studio Code (also known as VS Code), be aware of the following issues where Visual Studio behaves differently to other editors:

* [Triple click doesn't select whole line](https://developercommunity.visualstudio.com/t/fix-known-issues-in-word-wrap/351760)
* [Pressing End key twice doesn't move cursor to end of line](https://developercommunity.visualstudio.com/t/fix-known-issues-in-word-wrap/351760)

## Related content

[Features of the code editor](../writing-code-in-the-code-and-text-editor.md)