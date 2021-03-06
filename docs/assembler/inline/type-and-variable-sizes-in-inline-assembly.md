---
title: Satır İçi Derlemede Tür ve Değişken Boyutları
ms.date: 08/30/2018
ms.topic: reference
helpviewer_keywords:
- variables, length
- size, getting in inline assembly
- size
- LENGTH operator
- TYPE operator
- SIZE operator
- inline assembly, operators
- variables, type
- variables, size
ms.assetid: b62c2f2b-a7ad-4145-bae4-d890db86d348
ms.openlocfilehash: bc98c8561a7fd06f875781802558cdd7e71a67ec
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80169246"
---
# <a name="type-and-variable-sizes-in-inline-assembly"></a>Satır İçi Derlemede Tür ve Değişken Boyutları

**Microsoft 'a özgü**

**Uzunluk**, **Boyut**ve **tür** işleçleri satır içi derlemede sınırlı bir anlam taşır. `DUP` işleçle birlikte kullanılamaz (Mase yönergeleriyle veya işleçlerle veri tanımlayamadığınız için). Ancak bunları, C veya C++ değişkenlerin veya türlerin boyutunu bulmak için kullanabilirsiniz:

- **Length** işleci bir dizideki öğe sayısını döndürebilir. Dizi olmayan değişkenler için 1 değerini döndürür.

- **Size** Işleci bir C veya C++ değişkeninin boyutunu döndürebilir. Değişkenin boyutu, **uzunluğu** ve **türü**ürünüdür.

- **Tür** Işleci bir C veya C++ tür ya da değişken boyutunu döndürebilir. Değişken bir diziyse, **türü** dizideki tek bir öğenin boyutunu döndürür.

Örneğin, programınızın 8 öğeli bir **int** dizisi varsa,

```cpp
int arr[8];
```

Aşağıdaki C ve derleme ifadeleri `arr` ve öğelerinin boyutunu verir.

|__asm|C|Boyut|
|-------------|-------|----------|
|**Uzunluk** ARR|`sizeof`(ARR)/`sizeof`(ARR [0])|8|
|**Boyut** ARR|`sizeof`(ARR)|32|
|ARR **türü**|`sizeof`(ARR [0])|4|

**SON Microsoft 'a özgü**

## <a name="see-also"></a>Ayrıca bkz.

[__asm Bloklarında Bütünleştirilmiş Kod Dili Kullanma](../../assembler/inline/using-assembly-language-in-asm-blocks.md)<br/>
