---
title: Naked İşlevleri
ms.date: 11/04/2016
helpviewer_keywords:
- naked functions
- functions [C++], naked
- prolog code
- epilog code
ms.assetid: 2543c8af-00d4-4a2a-8a87-e746da1f9929
ms.openlocfilehash: b752dd6fa378bc1275e8a7da90420aa2b8247e4e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62232823"
---
# <a name="naked-functions"></a>Naked İşlevleri

**Microsoft'a Özgü**

`naked` depolama sınıfı özniteliği, C diline yönelik Microsoft'a özgü bir uzantıdır. `naked` depolama sınıfı özniteliğiyle bildirilen işlevler için derleyici giriş ve sonuç kodu olmadan kod oluşturur. Satır içi derleyici kodunu kullanarak kendi giriş/sonuç kodu dizilerinizi yazmak için bu özelliği kullanabilirsiniz. Çıplak işlevler, özellikle sanal cihaz sürücülerinin yazılmasında yararlıdır.

`naked` Özniteliği yalnızca bir işlevin tanımına uygun olduğundan ve bir tür değiştiricisi olmadığından, çıplak Işlevler [genişletilmiş depolama sınıfı öznitelikleri](../c-language/c-extended-storage-class-attributes.md)bölümünde açıklanan genişletilmiş öznitelik sözdizimini kullanır.

Aşağıdaki örnekte, `naked` özniteliğine sahip bir işlev tanımlanmaktadır:

```
__declspec( naked ) int func( formal_parameters )
{
   /* Function body */
}
```

Veya alternatif olarak:

```
#define Naked   __declspec( naked )

Naked int func( formal_parameters )
{
   /* Function body */
}
```

`naked` özniteliği, yalnızca işlevin giriş ve sonuç dizileri için derleyicinin kod oluşturma yapısını etkiler. Bu tür işlevleri çağırmak için oluşturulan kodu etkilemez. Bu nedenle, `naked` özniteliği işlev türünün bir parçası olarak kabul edilmez ve işlev işaretçileri `naked` özniteliğine sahip olamaz. Ayrıca, `naked` özniteliği veri tanımına uygulanamaz. Örneğin, aşağıdaki kod hatalar oluşturur:

```
__declspec( naked ) int i;  /* Error--naked attribute not */
                            /* permitted on data declarations. */
```

`naked` özniteliği, yalnızca işlevin tanımıyla ilgilidir ve işlevin prototipinde belirtilemez. Aşağıdaki bildirim, bir derleyici hatası oluşturur:

```
__declspec( naked ) int func();   /* Error--naked attribute not */
                     /* permitted on function declarations.    */   \
```

**SON Microsoft 'a özgü**

## <a name="see-also"></a>Ayrıca bkz.

[C İşlev Tanımları](../c-language/c-function-definitions.md)
