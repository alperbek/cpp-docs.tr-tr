---
title: RDX (C++ com özniteliği)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.rdx
helpviewer_keywords:
- rdx attribute
ms.assetid: ff8e4312-c1ad-4934-bdaa-86f54409651e
ms.openlocfilehash: f0140b759b1d78eb1284213a0dc47d9600b2a83b
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80214636"
---
# <a name="rdx"></a>rdx

Bir kayıt defteri anahtarı oluşturur veya var olan bir kayıt defteri anahtarını değiştirir.

## <a name="syntax"></a>Sözdizimi

```cpp
[ rdx(key, valuename=NULL, regtype) ]
```

### <a name="parameters"></a>Parametreler

*anahtar*<br/>
Oluşturulacak veya açılacak anahtarın adı.

*ValueName*<br/>
Seçim Ayarlanacak değer alanını belirtir. Bu ada sahip bir değer alanı anahtarda zaten yoksa, eklenir.

*regtype*<br/>
Eklenmekte olan kayıt defteri anahtarının türü. Aşağıdakilerden biri olabilir: `text`, `dword`, `binary`veya `CString`.

## <a name="remarks"></a>Açıklamalar

**RDX** C++ özniteliği bir com bileşeni için var olan bir kayıt defteri anahtarı oluşturur veya değiştirir. Özniteliği, hedef üyeyi uygulayan nesnesine bir BEGIN_RDX_MAP makrosu ekler. `RegistryDataExchange`, BEGIN_RDX_MAP makrosunun bir sonucu olarak eklenen bir işlev, kayıt defteri ve veri üyeleri arasında veri aktarmak için kullanılabilir

Bu öznitelik, [coclass](coclass.md), [ProgID](progid.md)veya [vi_progid](vi-progid.md) öznitelikleri ya da bunlardan birini belirten diğer özniteliklerle birlikte kullanılabilir.

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**Uygulama hedefi**|**sınıf** veya **Yapı** üyesi|
|**Tekrarlanabilir**|Hayır|
|**Gerekli öznitelikler**|Hiçbiri|
|**Geçersiz öznitelikler**|Hiçbiri|

Öznitelik bağlamları hakkında daha fazla bilgi için bkz. [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="example"></a>Örnek

Aşağıdaki kod, CMyClass COM bileşenini açıklayan sisteme MyValue adlı bir kayıt defteri anahtarı ekler.

```cpp
// cpp_attr_ref_rdx.cpp
// compile with: /LD /link /OPT:NOREF
#define _ATL_ATTRIBUTES
#include "atlbase.h"

[module (name="MyLib")];

class CMyClass {
public:
   CMyClass() {
      strcpy_s(m_sz, "SomeValue");
   }

   [ rdx(key = "HKCR\\MyApp.MyApp.1", valuename = "MyValue", regtype = "text")]
   char m_sz[256];
};
```

## <a name="see-also"></a>Ayrıca bkz.

[COM Öznitelikleri](com-attributes.md)<br/>
[registration_script](registration-script.md)
