---
title: Derleyici Uyarısı (düzey 3) C4265
ms.date: 11/04/2016
f1_keywords:
- C4265
helpviewer_keywords:
- C4265
ms.assetid: 20547159-6f30-4cc4-83aa-927884c8bb4c
ms.openlocfilehash: cfcbd9d9268785b87e45a833b332c276eec01522
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80161548"
---
# <a name="compiler-warning-level-3-c4265"></a>Derleyici Uyarısı (düzey 3) C4265

' class ': sınıf sanal işlevlere sahip, ancak yıkıcı sanal değil

Bir sınıfta sanal işlevler olduğunda ancak sanal olmayan bir yıkıcı olduğunda, sınıf bir temel sınıf işaretçisi aracılığıyla yok edildiğinde tür nesneleri düzgün şekilde yok edilmez.

Bu uyarı varsayılan olarak kapalıdır. Daha fazla bilgi için bkz. [Varsayılan olarak kapalı olan Derleyici uyarıları](../../preprocessor/compiler-warnings-that-are-off-by-default.md) .

Aşağıdaki örnek C4265 oluşturur:

```cpp
// C4265.cpp
// compile with: /W3 /c
#pragma warning(default : 4265)
class B
{
public:
   virtual void vmf();

   ~B();
   // try the following line instead
   // virtual ~B();
};   // C4265

int main()
{
   B b;
}
```
