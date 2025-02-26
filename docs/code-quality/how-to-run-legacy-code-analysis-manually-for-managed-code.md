---
title: Run legacy code analysis manually (.NET)
description: Learn how to detect possible defects in source code. See how to run legacy code analysis manually on managed code in Visual Studio.
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
  - code analysis, running
author: Mikejo5000
ms.author: mikejo
manager: mijacobs
ms.subservice: code-analysis

---

# Run legacy code analysis manually for managed code

The code analysis tool provides information to you about possible defects in your source code. You can run code analysis automatically with each build of a code project, and you can also run code analysis manually. The rules that are checked when code analysis is run are specified on the Code Analysis page of the project property pages. For more information, see [How to: Configure Code Analysis for a Managed Code Project](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md).

## To run code analysis manually

1. If you are on Visual Studio 2019 version 16.5 or later, execute the following command on command prompt before starting Visual Studio:

    `setx EnableLegacyCodeAnalysis true`

2. In **Solution Explorer**, click the project.

3. On the **Analyze** menu, click **Run Code Analysis on** *Project Name*.
