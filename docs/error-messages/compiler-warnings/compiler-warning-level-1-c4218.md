---
title: Derleyici Uyarısı (düzey 1) C4218
ms.date: 11/04/2016
f1_keywords:
- C4218
helpviewer_keywords:
- C4218
ms.assetid: d6c3cd90-4518-49e9-ae86-4ba9e2761d98
ms.openlocfilehash: f7553b30a17f50f559351353552fd656fceb8657
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80199803"
---
# <a name="compiler-warning-level-1-c4218"></a>Derleyici Uyarısı (düzey 1) C4218

Standart olmayan uzantı kullanıldı: en az bir depolama sınıfı veya türü belirtilmelidir

Varsayılan Microsoft uzantılarıyla (/Ze), bir tür veya depolama sınıfı belirtmeden bir değişken bildirebilirsiniz. Varsayılan tür `int`.

## <a name="example"></a>Örnek

```cpp
// C4218.c
// compile with: /W4
i;  // C4218

int main()
{
}
```

Bu bildirimler, ANSI uyumluluğu ([/za](../../build/reference/za-ze-disable-language-extensions.md)) altında geçersizdir.
