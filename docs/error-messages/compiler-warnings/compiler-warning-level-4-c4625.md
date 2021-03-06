---
title: Derleyici Uyarısı (düzey 4) C4625
ms.date: 11/04/2016
f1_keywords:
- C4625
helpviewer_keywords:
- C4625
ms.assetid: 4cc99e50-846c-4784-97da-48b977067851
ms.openlocfilehash: d98e295a9a48da16b58202bc172e112b5c0287d9
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74990718"
---
# <a name="compiler-warning-level-4-c4625"></a>Derleyici Uyarısı (düzey 4) C4625

' derived class ': bir taban sınıf kopya oluşturucusuna erişilemediğinden veya silindiğinden kopya Oluşturucu örtük olarak silindi olarak tanımlandı

Bir kopya Oluşturucu bir temel sınıfta silindi veya erişilebilir değil ve bu nedenle türetilmiş bir sınıf için üretilmedi. Bu türdeki bir nesneyi kopyalama girişimi, bir derleyici hatasına neden olur.

Bu uyarı varsayılan olarak kapalıdır. Daha fazla bilgi için bkz. [Varsayılan olarak kapalı olan Derleyici uyarıları](../../preprocessor/compiler-warnings-that-are-off-by-default.md) .

## <a name="example"></a>Örnek

Aşağıdaki örnek C4625 oluşturur ve nasıl düzeltileceğini gösterir.

```cpp
// C4625.cpp
// compile with: /W4 /c
#pragma warning(default : 4625)

struct A {
   A() {}

private:
   A(const A&) {}
};

struct C : private virtual A {};
struct B :  C {};   // C4625 no copy constructor

struct D : A {};
struct E :  D {};   // OK
```
