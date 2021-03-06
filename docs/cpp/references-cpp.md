---
title: Başvurular (C++)
ms.date: 11/04/2016
helpviewer_keywords:
- objects [C++], referencing
- references [C++]
- references, to pointers
- declarations, references
- references, declaring
- referencing objects, declarator syntax
ms.assetid: 68156f7f-97a0-4b66-b26d-b25ade5e3bd8
ms.openlocfilehash: 2353f0861f0f249416d0bb84a7a951b1cb6d64bc
ms.sourcegitcommit: a6d63c07ab9ec251c48bc003ab2933cf01263f19
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74857339"
---
# <a name="references-c"></a>Başvurular (C++)

Bir işaretçi gibi bir başvuru, bellekte başka bir yerde bulunan nesnenin adresini depolar. Bir işaretçinin aksine, başlatıldıktan sonra bir başvuru, farklı bir nesneye başvurmak veya null olarak ayarlamak için yapılamaz. İki tür başvuru vardır: bir adlandırılmış değişkene başvuran lvalue başvuruları ve [geçici bir nesneye](../cpp/temporary-objects.md)başvuran Rvalue başvuruları. & İşleci bir lvalue başvurusunu belirtir ve & & işleci, içeriğe bağlı olarak bir rvalue başvurusu ya da bir evrensel başvuru (rvalue ya da lvalue) belirtir.

Başvurular aşağıdaki sözdizimi kullanılarak bildirilebilecek:

> \[*Storage-Class-belirticileri*] \[*CV-niteleyicileri*] *tür-belirticileri* \[*ms-değiştirici*] *bildirimci* \[ **=** *ifadesi*] **;**

Bir başvuru belirten geçerli bir bildirimci kullanılabilir. Başvuru, işlev veya dizi türüne başvuru olmadığı takdirde, aşağıdaki Basitleştirilmiş sözdizimi geçerlidir:

> \[*Storage-Class-belirticileri*] \[*CV-niteleyicileri*] *tür-belirticileri* \[ **&** veya **&&** ] \[*CV-niteleyiciler*] *tanımlayıcı* \[ **=** *ifadesi*] **;**

Başvurular aşağıdaki sıra kullanılarak bildirilmiştir:

1. Bildirim tanımlayıcıları:

   - İsteğe bağlı bir depolama sınıfı belirleyicisi.

   - İsteğe bağlı **const** ve/veya **volatile** niteleyicileri.

   - Tür belirleyicisi: bir türün adı.

1. Bildirimci:

   - İsteğe bağlı Microsoft'a özgü bir değiştirici. Daha fazla bilgi için bkz. [Microsoft 'A özgü değiştiriciler](../cpp/microsoft-specific-modifiers.md).

   - **&** işleci veya **&&** işleci.

   - İsteğe bağlı **const** ve/veya **volatile** niteleyicilerinin.

   - Tanımlayıcı.

1. İsteğe bağlı bir başlatıcı.

Dizilere ve işlevlere işaretçiler için daha karmaşık bildirimci formları, dizilere ve işlevlere başvurular için de geçerlidir. Daha fazla bilgi için bkz. [işaretçiler](../cpp/pointers-cpp.md).

Birden çok Bildirimciler ve başlatıcılar, tek bir bildirim belirticisini izleyen virgülle ayrılmış bir listede görünebilir. Örneğin:

```cpp
int &i;
int &i, &j;
```

Başvurular, işaretçiler ve nesneler birlikte bildirilebilecek:

```cpp
int &ref, *ptr, k;
```

Başvuru bir nesnenin adresini tutar, ancak sözdizimi bir nesne gibi davranır.

Aşağıdaki programda, nesne adı, `s`ve `SRef`nesnesine başvuru, programlar içinde aynı şekilde kullanılabilir:

## <a name="example"></a>Örnek

```cpp
// references.cpp
#include <stdio.h>
struct S {
   short i;
};

int main() {
   S  s;   // Declare the object.
   S& SRef = s;   // Declare the reference.
   s.i = 3;

   printf_s("%d\n", s.i);
   printf_s("%d\n", SRef.i);

   SRef.i = 4;
   printf_s("%d\n", s.i);
   printf_s("%d\n", SRef.i);
}
```

```Output
3
3
4
4
```

## <a name="see-also"></a>Ayrıca bkz.

[Başvuru Türü İşlev Bağımsız Değişkenleri](../cpp/reference-type-function-arguments.md)<br/>
[Başvuru Türü İşlev Dönüşleri](../cpp/reference-type-function-returns.md)<br/>
[İşaretçi Başvuruları](../cpp/references-to-pointers.md)
