---
title: registration_script (C++ com özniteliği)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.registration_script
helpviewer_keywords:
- registration_script attribute
ms.assetid: 786f8072-9187-4163-a979-7a604dd4c888
ms.openlocfilehash: 780f3d41676d01458f47542d6f0862a278edff6a
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80214584"
---
# <a name="registration_script"></a>registration_script

Belirtilen özel kayıt betiğini yürütür.

## <a name="syntax"></a>Sözdizimi

```cpp
[ registration_script(script) ]
```

### <a name="parameters"></a>Parametreler

*SCRIPT*<br/>
Özel bir kayıt betiği (. RGS) dosyasının tam yolu. `script = "none"`gibi **none**değeri, coclass 'ın kayıt gereksinimlerini içermediğini gösterir.

## <a name="remarks"></a>Açıklamalar

**Registration_script** C++ özniteliği, *komut dosyası*tarafından belirtilen özel kayıt betiğini yürütür. Bu öznitelik belirtilmemişse, standart bir. rgs dosyası (bileşeni kaydetmek için bilgi içeren) kullanılır. . Rgs dosyaları hakkında daha fazla bilgi için bkz. [atl kayıt defteri bileşeni (kaydedici)](../../atl/atl-registry-component-registrar.md).

Bu öznitelik, [coclass](coclass.md), [ProgID](progid.md)veya [vi_progid](vi-progid.md) özniteliğinin (ya da bunlardan birini belirten başka bir özniteliğin) aynı öğeye uygulanmasını gerektirir.

## <a name="example"></a>Örnek

Aşağıdaki kod, bileşenin cpp_attr_ref_registration_script. rgs adlı bir kayıt defteri betiğinin bulunduğunu belirtir.

```cpp
// cpp_attr_ref_registration_script.cpp
// compile with: /LD
#define _ATL_ATTRIBUTES
#include "atlbase.h"
#include "atlcom.h"

[module (name="REG")];

[object, uuid("d9cd196b-6836-470b-9b9b-5b04b828e5b0")]
__interface IFace {};

// requires "cpp_attr_ref_registration_script.rgs"
// create sample .RGS file "cpp_attr_ref_registration_script.rgs" if it does not exist
[ coclass, registration_script(script="cpp_attr_ref_registration_script.rgs"),
  uuid("50d3ad42-3601-4f26-8cfe-0f1f26f98f67")]
class CMyClass:public IFace {};
```

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**Uygulama hedefi**|**sınıf**, **Yapı**|
|**Tekrarlanabilir**|Hayır|
|**Gerekli öznitelikler**|Aşağıdakilerden biri veya daha fazlası: `coclass`, `progid`veya `vi_progid`.|
|**Geçersiz öznitelikler**|Hiçbiri|

Öznitelik bağlamları hakkında daha fazla bilgi için bkz. [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>Ayrıca bkz.

[COM Öznitelikleri](com-attributes.md)<br/>
[Sınıf Öznitelikleri](class-attributes.md)<br/>
[rdx](rdx.md)
