---
title: Derleyici hatası C3642
ms.date: 11/04/2016
f1_keywords:
- C3642
helpviewer_keywords:
- C3642
ms.assetid: 429790c2-9614-4d85-b31c-687c8d8f83ff
ms.openlocfilehash: 7c3f9f05bf04c9a1c20fff7910836e7b50468a8e
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74742463"
---
# <a name="compiler-error-c3642"></a>Derleyici hatası C3642

' return_type/args ': yerel koddan __clrcall çağırma kuralına sahip bir işlev çağrılamaz

[__Clrcall](../../cpp/clrcall.md) çağırma kuralıyla işaretlenen bir işlev yerel (yönetilmeyen) koddan çağrılamaz.

*return_type/args* işlevin adı ya da çağırmaya çalıştığınız `__clrcall` işlevin türüdür.  Bir tür, bir işlev işaretçisi aracılığıyla çağrılırken kullanılır.

Yerel bağlamdan yönetilen bir işlevi çağırmak için `__clrcall` işlevini çağıracak bir "sarmalayıcı" işlevi ekleyebilirsiniz. Ya da, CLR sıralama mekanizmasını kullanabilirsiniz; daha fazla bilgi için bkz. [nasıl yapılır: PInvoke kullanarak Işlev Işaretçilerini sıralama](../../dotnet/how-to-marshal-function-pointers-using-pinvoke.md) .

Aşağıdaki örnek C3642 oluşturur:

```cpp
// C3642.cpp
// compile with: /clr
using namespace System;
struct S {
   void Test(String ^ s) {   // CLR type in signature, implicitly __clrcall
      Console::WriteLine(s);
   }
   void Test2(char * s) {
      Test(gcnew String(s));
   }
};

#pragma unmanaged
int main() {
   S s;
   s.Test("abc");   // C3642
   s.Test2("abc");   // OK
}
```
