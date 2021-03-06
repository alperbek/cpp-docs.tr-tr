---
title: Derleyici hatası C3851
ms.date: 09/05/2018
f1_keywords:
- C3851
helpviewer_keywords:
- C3851
ms.assetid: da30c21c-33aa-4439-8fb3-2f5021ea4985
ms.openlocfilehash: 97d9ef1eeeffa0e5a63d2c8ae2428a3fad0ff238
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80165593"
---
# <a name="compiler-error-c3851"></a>Derleyici hatası C3851

> '*char*': bir evrensel karakter adı temel karakter kümesindeki bir karakteri belirleyemez

## <a name="remarks"></a>Açıklamalar

Olarak C++derlenen kodda, bir dize veya karakter sabiti dışında temel kaynak karakter kümesindeki bir karakteri temsil eden bir evrensel karakter adı kullanamazsınız. Daha fazla bilgi için bkz. [karakter kümeleri](../../cpp/character-sets.md). C olarak derlenen kodda, 0x20-0x7F aralığında, 0x24 (' $ '), 0x40 ('\@') veya 0x60 ('\`') dışındaki karakterler için evrensel karakter adı kullanamazsınız.

## <a name="example"></a>Örnek

Aşağıdaki örnekler C3851 oluşturur ve nasıl düzeltileceğini gösterir:

```cpp
// C3851.cpp
int main()
{
   int test1_\u0041 = 0;   // C3851, \u0041 = 'A' in basic character set
   int test2_A = 0;        // OK
}
```
