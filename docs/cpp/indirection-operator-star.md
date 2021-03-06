---
title: 'Yönlendirme İşleci: *'
ms.date: 11/04/2016
helpviewer_keywords:
- '* operator'
- indirection operator
- operators [C++], indirection
- indirection operator [C++], syntax
ms.assetid: c50309e1-6c02-4184-9fcb-2e13c1f4ac03
ms.openlocfilehash: 8f27cfd943455d52b04c41ef2d2d83e6e03a84c0
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80178292"
---
# <a name="indirection-operator-"></a>Yönlendirme İşleci: *

## <a name="syntax"></a>Sözdizimi

```
* cast-expression
```

## <a name="remarks"></a>Açıklamalar

Birli yöneltme işleci (<strong>\*</strong>) bir işaretçiye başvurur; Yani, bir işaretçi değerini bir l değerine dönüştürür. Yöneltme işlecinin işleneni, bir tür işaretçisi olmalıdır. Yöneltme ifadesinin sonucu, işaretçi türünün türetildiği türüdür. <strong>\*</strong> işlecinin bu bağlamda kullanımı, çarpının, çarpma olan bir ikili işleç olarak farklıdır.

İşlenen bir işleve işaret ediyorsa, sonuç bir işlev göstergesidir. Bir depolama konumuna işaret ediyorsa, sonuç depolama konumunu gösteren l değeridir.

Yöneltme işleci, işaretçilere yönelik işaretçileri başvurusu için üst üste kullanılabilir. Örneğin:

```cpp
// expre_Indirection_Operator.cpp
// compile with: /EHsc
// Demonstrate indirection operator
#include <iostream>
using namespace std;
int main() {
   int n = 5;
   int *pn = &n;
   int **ppn = &pn;

   cout  << "Value of n:\n"
         << "direct value: " << n << endl
         << "indirect value: " << *pn << endl
         << "doubly indirect value: " << **ppn << endl
         << "address of n: " << pn << endl
         << "address of n via indirection: " << *ppn << endl;
}
```

İşaretçi değeri geçersizse, sonuç tanımsızdır. Aşağıdaki liste, işaretçi değerini geçersiz kılan en yaygın koşulların bazılarını içermektedir.

- İşaretçi, bir null işaretçidir.

- İşaretçi, başvuru sırasında görünür olmayan yerel bir öğrenin adresini belirtir.

- İşaretçi, işaret edilen nesnenin türü için uygun olmayan bir şekilde hizalanmış bir adresi belirtir.

- İşaretçi, yürütülen program tarafından kullanılmayan bir adresi belirtir.

## <a name="see-also"></a>Ayrıca bkz.

[Birli İşleçli İfadeler](../cpp/expressions-with-unary-operators.md)<br/>
[C++ Yerleşik İşleçler, Öncelik ve İlişkisellik](../cpp/cpp-built-in-operators-precedence-and-associativity.md)<br/>
[Address-of İşleci: &](../cpp/address-of-operator-amp.md)<br/>
[İşleçlerin Yöneltmesi ve Adresi](../c-language/indirection-and-address-of-operators.md)
