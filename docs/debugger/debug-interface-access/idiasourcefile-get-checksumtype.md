---
description: "Retrieves the checksum type."
title: "IDiaSourceFile::get_checksumType"
ms.date: "11/04/2016"
ms.topic: "reference"
dev_langs:
  - "C++"
helpviewer_keywords:
  - "IDiaSourceFile::get_checksumType method"
author: "mikejo5000"
ms.author: "mikejo"
manager: jmartens
ms.subservice: debug-diagnostics
---
# IDiaSourceFile::get_checksumType

Retrieves the checksum type.

## Syntax

```C++
HRESULT get_checksumType ( 
   DWORD* pRetVal
);
```

#### Parameters
 `pRetVal`

[out] Returns the checksum type.

## Return Value
 If successful, returns `S_OK`; otherwise, returns an error code.

## Remarks
 The checksum type is a value that can be mapped to a checksum algorithm. For example, the standard PDB file format can typically have one of the following values:

|Checksum Type|CryptoAPI Label|Description|
|-------------------|---------------------|-----------------|
|0|\<none>|No checksum present.|
|1|`CALG_MD5`|checksum generated with the MD5 hashing algorithm.|
|2|`CALG_SHA1`|checksum generated with the SHA1 hashing algorithm.|

 The `CryptoAPI` labels are from the `ALG_ID` enumeration. For more information on hashing algorithms, consult the `CryptoAPI` section of the Microsoft Windows SDK.

 To obtain the actual checksum bytes for the source file, call the [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md) method.

## See also
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)
