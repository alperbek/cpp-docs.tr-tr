---
title: Bağlayıcı Araçları Hatası LNK2028
ms.date: 11/04/2016
f1_keywords:
- LNK2028
helpviewer_keywords:
- LNK2028
ms.assetid: e2b03293-6066-464d-a050-ce747bcf7f0e
ms.openlocfilehash: ef9e3eae655a4fbee1c3da74f6036e5fb22434b1
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80194622"
---
# <a name="linker-tools-error-lnk2028"></a>Bağlayıcı Araçları Hatası LNK2028

"*function_containing_function_call*" işlevinde "*exported_function*" (*decorated_name*) başvuruluyor (*decorated_name*)

## <a name="remarks"></a>Açıklamalar

Yerel bir işlevi saf bir görüntüye aktarmaya çalışırken, örtük çağırma kurallarının yerel ve saf derlemeler arasında farklı olduğunu unutmayın.

**/Clr: Pure** derleyici seçeneği visual Studio 2015 ' de kullanımdan kaldırılmıştır ve visual Studio 2017 ' de desteklenmez.

## <a name="example"></a>Örnek

Bu kod örneği,, çağıran kuralı örtük olarak [__cdecl](../../cpp/cdecl.md), dışarıya aktarılmış, yerel, işlevi olan bir bileşen oluşturur.

```cpp
// LNK2028.cpp
// compile with: /LD
__declspec(dllexport) int func() {
   return 3;
}
```

## <a name="example"></a>Örnek

Aşağıdaki örnek, yerel işlevi tüketen bir saf istemci oluşturur. Ancak, **/clr: Pure** altındaki çağırma kuralı [__clrcall](../../cpp/clrcall.md). Aşağıdaki örnek LNK2028 oluşturur.

```cpp
// LNK2028_b.cpp
// compile with: /clr:pure lnk2028.lib
// LNK2028 expected
int func();

int main() {
   return func();
}
```
