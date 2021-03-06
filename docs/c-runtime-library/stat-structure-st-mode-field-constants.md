---
title: _stat Yapı st_mode Alanı Sabitleri
ms.date: 11/04/2016
f1_keywords:
- S_IFCHR
- S_IFDIR
- _S_IWRITE
- S_IFMT
- _S_IFDIR
- _S_IREAD
- S_IEXEC
- _S_IEXEC
- _S_IFMT
- S_IWRITE
- S_IFREG
- S_IREAD
- _S_IFCHR
- _S_IFREG
helpviewer_keywords:
- S_IFDIR constant
- stat structure
- S_IWRITE constant
- S_IEXEC constant
- _S_IFREG constant
- S_IREAD constant
- stat structure, constants
- _S_IFMT constant
- st_mode field constants
- S_IFMT constant
- _S_IEXEC constant
- _S_IWRITE constant
- _S_IFDIR constant
- S_IFREG constant
- S_IFCHR constant
- _S_IREAD constant
- _S_IFCHR constant
ms.assetid: fd462004-7563-4766-8443-30b0a86174b6
ms.openlocfilehash: ff2b6ac806b774ae3fe80f9b3cf4b3d2e82a2a9c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62267851"
---
# <a name="stat-structure-stmode-field-constants"></a>_stat Yapı st_mode Alanı Sabitleri

## <a name="syntax"></a>Sözdizimi

```
#include <sys/stat.h>
```

## <a name="remarks"></a>Açıklamalar

Bu sabitler dosya türünü belirtmek için kullanılan **st_mode** alanını [_stat yapı](../c-runtime-library/standard-types.md).

Bit maskesi sabitleri aşağıda açıklanmıştır:

|Sabit|Açıklama|
|--------------|-------------|
|`_S_IFMT`|Dosya türü maskesi|
|`_S_IFDIR`|Dizin|
|`_S_IFCHR`|Özel karakter (bir cihaz belirtir ayarlayın)|
|`_S_IFREG`|Normal|
|`_S_IREAD`|Okuma izni, sahibi|
|`_S_IWRITE`|Yazma izni, sahibi|
|`_S_IEXEC`|Yürütme/arama iznine sahibi|

## <a name="see-also"></a>Ayrıca bkz.

[_stat, _wstat işlevleri](../c-runtime-library/reference/stat-functions.md)<br/>
[_fstat, _fstat32, _fstat64, _fstati64, _fstat32i64, _fstat64i32](../c-runtime-library/reference/fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)<br/>
[Standart Türler](../c-runtime-library/standard-types.md)<br/>
[Global Sabitler](../c-runtime-library/global-constants.md)
