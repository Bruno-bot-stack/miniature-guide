---
title: Run code analysis manually for .NET
ms.date: 05/13/2022
description: "Learn how to manually run code analysis in Visual Studio 2019 version 16.5 or later versions. See how to run Roslyn analyzers on C# or Visual Basic code."
ms.topic: how-to
helpviewer_keywords:
  - code analysis, running
  - run code analysis
author: mikadumont
ms.author: midumont
manager: mijacobs
ms.subservice: code-analysis
---
# Run code analysis manually for .NET

By default, .NET Compiler Platform ("Roslyn") analyzers analyze your C# or Visual Basic code as you type by doing live analysis, as well as during build. Hence, you won't normally need to trigger code analysis manually. However, there are some scenarios where you may want to manually trigger code analysis:

- By default, live code analysis executes analyzers only for the active document in Visual Studio 2022 and later versions. However, you may be interested in viewing code analysis warnings for all files in a specific project or solution. If so, you would want to trigger code analysis once on a project or a solution. Alternatively, you can enable continuous live code analysis to execute on the entire solution. For more information, see [How to: Configure live code analysis scope for managed code](./configure-live-code-analysis-scope-managed-code.md).
- You may prefer on-demand code analysis execution workflow over continuous live analysis or build-time analysis. If so, you can disable analyzer execution during live analysis and/or build. For information about disabling analysis, see [How to disable source code analysis](disable-code-analysis.md). Then you can manually trigger code analysis once on a project or solution.

> [!NOTE]
> Running code analysis manually requires Visual Studio 2019 version 16.5 or later

## Run code analysis manually

1. In **Solution Explorer**, select the project.

2. On the **Analyze** menu, select **Run Code Analysis on [Project Name]**.

Code analysis will start executing in the background. You should see the message **Running code analysis for \<project>** in the Visual Studio status bar towards the bottom-left corner. Once code analysis completes, the status message will change to **Code analysis completed for \<project>**. Error list will soon refresh with all code analysis diagnostics.
