---
title: Derleyici Uyarısı (düzey 3) C4414
ms.date: 11/04/2016
f1_keywords:
- C4414
helpviewer_keywords:
- C4414
ms.assetid: bc81d3ad-55dc-4a6b-a6f2-ec0ef38347df
ms.openlocfilehash: 4625f6bdb4aa6fe86ca881a8e36e5673e55ccb87
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80185600"
---
# <a name="compiler-warning-level-3-c4414"></a>Derleyici Uyarısı (düzey 3) C4414

' function ': işleve yönelik kısa zıplama yakın olarak dönüştürüldü

Kısa atlamaları, yönergeden sınırlı bir aralıktaki bir adrese dalların dallarından oluşan kompakt yönerge oluşturur. Yönerge, işlev tanımı olan zıplama ve hedef adres arasındaki mesafeyi temsil eden bir kısa uzaklık içerir. Bir işlevi bağlama sırasında, işlevin kısa bir uzaklığa göre erişilebilen aralıktan taşınmasına neden olan bağlantı zaman iyileştirmeleri taşınabilir veya bu duruma tabi olabilir. Derleyici, konumuna JMP yönergesinin YAKıNıNDA veya en uzak olmasını gerektiren, atlamanın özel bir kaydını üretmelidir. Derleyici dönüştürmeyi yaptı.

Örneğin, aşağıdaki kod C4414 oluşturur:

```cpp
// C4414.cpp
// compile with: /W3 /c
// processor: x86
int DoParityEven();
int DoParityOdd();
unsigned char global;
int __declspec(naked) DoParityEither()
{
   __asm
   {
      test global,0
      jpe SHORT DoParityEven  // C4414
      jmp SHORT DoParityOdd   // C4414
   }
}
```
