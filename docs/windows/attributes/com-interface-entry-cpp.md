---
title: com_interface_entry (C++ com özniteliği)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.com_interface_entry
helpviewer_keywords:
- com_interface_entry attribute
ms.assetid: 10368f81-b99b-4a0f-ba4f-a142e6911a5c
ms.openlocfilehash: d7b378baedd3f8c2720c7ab17698e8b416304061
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80168310"
---
# <a name="com_interface_entry-c"></a>com_interface_entry (C++)

Hedef sınıfın COM eşlemesine bir arabirim girişi ekler.

## <a name="syntax"></a>Sözdizimi

```cpp
[ com_interface_entry(
  com_interface_entry) ]
```

### <a name="parameters"></a>Parametreler

*com_interface_entry*<br/>
Girişin gerçek metnini içeren bir dize. Olası değerler listesi için bkz. [COM_INTERFACE_ENTRY makroları](../../atl/reference/com-interface-entry-macros.md).

## <a name="remarks"></a>Açıklamalar

**Com_interface_entry** C++ özniteliği, bir karakter dizesinin bilinişsiz içeriğini hedef nesnenin com arabirim eşlemesine ekler. Öznitelik hedef nesneye bir kez uygulanırsa, giriş varolan arabirim eşlemesinin başlangıcına eklenir. Özniteliği aynı hedef nesneye tekrar tekrar uygulanırsa, girdiler alındıkları sırada arabirim eşlemesinin başına eklenir.

Bu öznitelik, [coclass](coclass.md), [ProgID](progid.md)veya [vi_progid](vi-progid.md) özniteliğinin (ya da bunlardan birini belirten başka bir özniteliğin) aynı öğeye uygulanmasını gerektirir. Tek bir öznitelik kullanılırsa, diğer ikisi otomatik olarak uygulanır. Örneğin, `progid` uygulanmışsa `vi_progid` ve `coclass` de uygulanır.

**Com_interface_entry** ilk kullanımı yeni arabirimin arabirim eşlemesinin başına eklenmesine neden olduğundan, aşağıdaki COM_INTERFACE_ENTRY türlerinden biri olmalıdır:

- COM_INTERFACE_ENTRY

- COM_INTERFACE_ENTRY_IID

- COM_INTERFACE_ENTRY2

- COM_INTERFACE_ENTRY2_IID

**Com_interface_entry** özniteliğin ek kullanımları desteklenen tüm COM_INTERFACE_ENTRY türlerini kullanabilir.

Bu kısıtlama gereklidir çünkü ATL, arabirim eşlemesindeki ilk girdiyi kimlik `IUnknown`olarak kullanıyor. Bu nedenle, giriş geçerli bir arabirim olmalıdır. Örneğin, arabirim eşlemesindeki ilk giriş gerçek bir COM arabirimi belirtmediğinden aşağıdaki kod örneği geçersizdir.

```cpp
[ coclass, com_interface_entry =
    "COM_INTERFACE_ENTRY_NOINTERFACE(IDebugTest)"
]
   class CMyClass
   {
   };
```

## <a name="example"></a>Örnek

Aşağıdaki kod, `CMyBaseClass`mevcut COM arabirimi eşlemesine iki giriş ekler. Birincisi standart bir arabirimdir ve ikincisi `IDebugTest` arabirimini gizler.

```cpp
// cpp_attr_ref_com_interface_entry.cpp
// compile with: /LD
#define _ATL_ATTRIBUTES
#include "atlbase.h"
#include "atlcom.h"

[module (name ="ldld")];

[ object,
  uuid("7dbebed3-d636-4917-af62-c767a720a5b9")]
__interface IDebugTest{};

[ object,
  uuid("2875ceac-f94b-4087-8e13-d13dc167fcfc")]
__interface IMyClass{};

[ coclass,
  com_interface_entry ("COM_INTERFACE_ENTRY (IMyClass)"),
  com_interface_entry ("COM_INTERFACE_ENTRY_NOINTERFACE(IDebugTest)"),
  uuid("b85f8626-e76e-4775-b6a0-4826a9e94af2")
]

class CMyClass: public IMyClass, public IDebugTest
{
};
```

`CMyBaseClass` için elde edilen COM nesne eşlemesi aşağıdaki gibidir:

```cpp
BEGIN_COM_MAP(CMyClass)
    COM_INTERFACE_ENTRY (IMyClass)
    COM_INTERFACE_ENTRY_NOINTERFACE(IDebugTest)
    COM_INTERFACE_ENTRY(IMyClass)
    COM_INTERFACE_ENTRY2(IDispatch, IMyClass)
    COM_INTERFACE_ENTRY(IDebugTest)
    COM_INTERFACE_ENTRY(IProvideClassInfo)
END_COM_MAP()
```

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**Uygulama hedefi**|**sınıf**, **Yapı**|
|**Tekrarlanabilir**|Yes|
|**Gerekli öznitelikler**|Aşağıdakilerden biri veya daha fazlası: `coclass`, `progid`veya `vi_progid`.|
|**Geçersiz öznitelikler**|Hiçbiri|

Öznitelik bağlamları hakkında daha fazla bilgi için bkz. [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>Ayrıca bkz.

[COM Öznitelikleri](com-attributes.md)<br/>
[Sınıf Öznitelikleri](class-attributes.md)<br/>
[Typedef, Enum, Union ve Struct Öznitelikleri](typedef-enum-union-and-struct-attributes.md)
