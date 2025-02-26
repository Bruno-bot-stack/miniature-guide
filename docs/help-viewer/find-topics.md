---
title: Search for topics (Help Viewer)
description: Learn how to search for topics in the Microsoft Help Viewer. Customize searches by using wildcard expressions, logical operators, and advanced search operators.
ms.date: 05/17/2022
ms.topic: how-to
author: jasonchlus
ms.author: jasonchlus
manager: mijacobs
ms.subservice: help-viewer
---
# Search for topics in Help Viewer

You can use the full-text search feature of Microsoft Help Viewer to locate all topics that contain a particular word. You can also refine and customize your search by using wildcard expressions, logical operators, and advanced search operators.

## To perform a full-text search

1. Use one of these methods to open the Help Viewer **Search** tab:

   - In the **Help Viewer** window, select the **Search** tab.
   - On the keyboard, select **Ctrl**+**E**.

1. In the search box, enter the word that you want to find.

1. In the search query, specify any logical or advanced search operators that you'd like to apply to the search. To search all available help, don't use operators.

    > [!NOTE]
    > In the **Viewer Options** dialog box, you can specify additional preferences such as the maximum number of search results to display at a time and whether to include English content if your primary locale isn't English.

1. Select the **Enter** key.

     A search returns a maximum of 200 hits, by default, and displays them in the search results area. Version information for each result may appear, depending on the content.

1. To view a topic, select its title from the results list.

## Full-text search tips

You can create more targeted searches that return only those topics that interest you, if you understand how syntax affects your query. The syntax includes special characters, reserved words, and filters. This section provides tips, procedures, and detailed syntax information to help you better craft your queries.

### General guidelines

The following table includes some basic rules and guidelines for developing search queries in help.

|Syntax|Description|
|------------|-----------------|
|Case sensitivity|Searches aren't case-sensitive. Develop your search criteria by using uppercase or lowercase characters. For example, "OLE" and "ole" return the same results.|
|Character combinations|You can't search only for individual letters (a-z) or numbers (0-9). If you try to search for certain reserved words, such as "and," "from," and "with," they're ignored. For more information, see [Words ignored in searches](#words-ignored-in-searches-stop-words) later in this article.|
|Evaluation order|Search queries are evaluated from left to right.|

### Search syntax

You might enter a search string that includes multiple words, such as "word1 word2." That string is equivalent to typing "word1 AND word2." Searches that use the AND operator return only topics that contain all the individual words in the search string.

> [!IMPORTANT]
> - Phrase searches are not supported. If you specify more than one word in a search string, returned topics contain all the words that you specified but not necessarily the exact phrase that you specified.
> - Use logical operators to specify the relationship between words in your search phrase. You can include logical operators, such as AND, OR, NOT, and NEAR, to further refine your search. For example, if you search for "declaring NEAR union", search results include topics that contain the words "declaring" and "union" no more than a few words apart from each other. For more information, see [Logical operators in search expressions](../help-viewer/logical-operators-search-expressions.md).

### Filters

You can further restrict search results by using advanced search operators. Help includes three categories that you can use to filter results of a full-text search: Title, Code, and Keyword.

### Ranking of search results

The search algorithm applies certain criteria to help rank search results higher or lower in the results list. In general:

- Content that includes search words in the title is ranked higher than content that doesn't.

- Content that includes search words in close proximity is ranked higher than content that doesn't.

- Content that contains a higher density of the search words is ranked higher than content that has a lower density of the search words.

### Words ignored in searches (stop words)

Commonly occurring words or numbers, which are sometimes called stop words, are automatically ignored during a full-text search. For example, if you search for the phrase "pass through," search results display topics that contain the word "pass" but not "through."

## See also

- [Logical and advanced operators](../help-viewer/logical-operators-search-expressions.md)
- [How to: Find topics in the index](../help-viewer/find-topics-index.md)
- [How to: Find topics in the TOC](../help-viewer/find-topics-toc.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)