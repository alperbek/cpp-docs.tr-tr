---
title: Bildirimler ve Tanımlar (C)
ms.date: 11/04/2016
helpviewer_keywords:
- export functions
ms.assetid: d150395a-89d4-4298-9ac4-08f84fe1261c
ms.openlocfilehash: 8723c3f09a5e9a8eecf0e552c9f5a7fd9b7f6c68
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62234364"
---
# <a name="definitions-and-declarations-c"></a>Bildirimler ve Tanımlar (C)

**Microsoft'a Özgü**

DLL arabirimi, sistemdeki bazı programlar tarafından verilmesi bilinen tüm öğeler (işlevler ve veriler) anlamına gelir; diğer bir deyişle, **dllimport** veya `dllexport`olarak belirtilen tüm öğeler. DLL arabirimine dahil edilen tüm bildirimlerin **dllimport** veya `dllexport` Attribute belirtmesi gerekir. Ancak, tanım yalnızca `dllexport` özniteliğini belirtebilir. Örneğin, aşağıdaki işlev tanımı bir derleyici hatası oluşturur:

```
#define DllImport   __declspec( dllimport )
#define DllExport   __declspec( dllexport )

DllImport int func()    /* Error; dllimport prohibited in */
                        /* definition. */
{
   return 1;
}
```

Bu kod, aynı zamanda bir hata oluşturur:

```
#define DllImport   __declspec( dllimport )
#define DllExport   __declspec( dllexport )

DllImport int i = 10;      /* Error; this is a definition. */
```

Bununla birlikte, doğru sözdizimi şöyledir:

```
#define DllImport   __declspec( dllimport )
#define DllExport   __declspec( dllexport )

DllExport int i = 10;      /* Okay: this is an export definition. */
```

Kullanımı bir tanım `dllexport` anlamına gelir, **dllimport** bir bildirimi gösterir. Bir bildirimi zorlamak için `extern` ile `dllexport` anahtar sözcüğünü kullanmanız gerekir; aksi takdirde, bir tanım gösterilir.

```
#define DllImport   __declspec( dllimport )
#define DllExport   __declspec( dllexport )

extern DllImport int k;   /* These are correct and imply */
Dllimport int j;          /* a declaration. */
```

**SON Microsoft 'a özgü**

## <a name="see-also"></a>Ayrıca bkz.

[DLL İçeri ve Dışarı Aktarma İşlevleri](../c-language/dll-import-and-export-functions.md)
