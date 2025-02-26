---
title: Specify custom build events
description: Explore how you can you can automatically run commands in Visual Studio before you start a build of your project or solution or after a build completes.
ms.date: 11/04/2016
ms.subservice: compile-build
ms.topic: conceptual
helpviewer_keywords:
- build events, customizing
author: ghogen
ms.author: ghogen
manager: jmartens
---
# Specify custom build events in Visual Studio

By specifying a custom build event, you can automatically run commands before a build starts or after it finishes. For example, you can run a *.bat* file before a build starts or copy new files to a folder after the build is complete. Build events run only if the build successfully reaches those points in the build process.

For specific information about the programming language that you're using, see the following topics:

- Visual Basic--[How to: Specify build events (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md).

- C# and F#--[How to: Specify build events (C#)](../ide/how-to-specify-build-events-csharp.md).

- Visual C++--[Specify build events](/cpp/build/specifying-build-events).

## Syntax

Build events follow the same syntax as DOS commands, but you can use macros to create build events more easily. For a list of available macros, see [Pre-build Event/Post-build Event command line dialog box](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md).

For best results, follow these formatting tips:

- Add a `call` statement before all build events that run *.bat* files.

   Example: `call C:\MyFile.bat`

   Example: `call C:\MyFile.bat call C:\MyFile2.bat`

- Enclose file paths in quotation marks.

   Example (for Windows 8): "%ProgramFiles(x86)%\Microsoft SDKs\Windows\v8.0A\Bin\NETFX 4.0 Tools\gacutil.exe" -if "$(TargetPath)"

- Separate multiple commands by using line breaks.

- Include wildcards as needed.

   Example: `for %I in (*.txt *.doc *.html) do copy %I c:\`*mydirectory*`\`

  > [!NOTE]
  > `%I` in the code above should be `%%I` in batch scripts.

## Related content

- [Compile and build](../ide/compiling-and-building-in-visual-studio.md)
- [Pre-build Event/Post-build Event command line dialog box](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [MSBuild special characters](../msbuild/msbuild-special-characters.md)
- [Walkthrough: Build an application](../ide/walkthrough-building-an-application.md)
