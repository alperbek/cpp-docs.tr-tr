---
title: Derleyici Uyarısı (düzey 4) C4389
ms.date: 11/04/2016
f1_keywords:
- c4389
helpviewer_keywords:
- C4389
ms.assetid: fc0e3a8e-f766-437c-b7f1-e61abb2a8765
ms.openlocfilehash: 94c9e6a49296ac048437501b1e61ddbd3e0ccbad
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74990863"
---
# <a name="compiler-warning-level-4-c4389"></a>Derleyici Uyarısı (düzey 4) C4389

' operator ': imzalı/imzasız uyuşmazlığı

İmzalı ve işaretsiz değişkenler ile ilgili bir işlem. Bu, veri kaybına neden olabilir.

Aşağıdaki örnek C4389 oluşturur:

```cpp
// C4389.cpp
// compile with: /W4
#pragma warning(default: 4389)

int main()
{
   int a = 9;
   unsigned int b = 10;
   if (a == b)   // C4389
      return 0;
   else
      return 0;
};
```
