---
title: Tam Sayıların İndirgenmesi
ms.date: 11/04/2016
helpviewer_keywords:
- demoting integers
ms.assetid: 51fb3654-60b0-4de7-80eb-bd910086c18a
ms.openlocfilehash: edfb8f03094c10cf0cf33b0eb799d5d822ac017d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62234411"
---
# <a name="demotion-of-integers"></a>Tam Sayıların İndirgenmesi

**ANSI 3.2.1.2** Bir tamsayıyı daha kısa işaretli bir tamsayıya dönüştürmenin sonucu veya işaretsiz bir tamsayıyı, değer temsil edilene eşit uzunlukta işaretli bir tamsayıya dönüştürme sonucu

**Uzun** bir tamsayı bir **Short**değerine ayarlandığında veya bir **Short** öğesine ayarlandığında `char`, en az önemli baytlar korunur.

Örneğin, bu satır

```
short x = (short)0x12345678L;
```

0x5678 değerini `x`'e atar ve bu satır

```
char y = (char)0x1234;
```

0x34 değerini `y`'ye atar.

İşaretli değişkenler işaretsiz değişkenlere ve işaretsiz değişkenler işaretli değişkenlere dönüştürüldüğünde, bit düzenleri aynı kalır. Örneğin,-2 (0xFE) işaretsiz bir değere 254 (Ayrıca 0xFE) verir.

## <a name="see-also"></a>Ayrıca bkz.

[Tam Sayılar](../c-language/integers.md)
