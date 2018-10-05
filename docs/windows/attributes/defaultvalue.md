---
title: DefaultValue (C++ COM özniteliği) | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.technology:
- cpp-windows
ms.topic: reference
f1_keywords:
- vc-attr.defaultvalue
dev_langs:
- C++
helpviewer_keywords:
- defaultvalue attribute
ms.assetid: efa5d050-b2cc-4d9e-9b8e-79954f218d3a
author: mikeblome
ms.author: mblome
ms.workload:
- cplusplus
- uwp
ms.openlocfilehash: e67ed063030ae619124d82cb8fb8de3e7a6ff708
ms.sourcegitcommit: 955ef0f9d966e7c9c65e040f1e28fa83abe102a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48789582"
---
# <a name="defaultvalue"></a>defaultvalue

Belirtilmiş bir isteğe bağlı parametre için bir varsayılan değer belirtimi sağlar.

## <a name="syntax"></a>Sözdizimi

```cpp
[ defaultvalue= value ]
```

### <a name="parameters"></a>Parametreler

*value*<br/>
Parametre için varsayılan değer.

## <a name="remarks"></a>Açıklamalar

**Defaultvalue** C++ özniteliği ile aynı işlevlere sahip [defaultvalue](/windows/desktop/Midl/defaultvalue) MIDL özniteliği.

## <a name="example"></a>Örnek

Aşağıdaki kod, bir arabirim yöntemini kullanarak göstermektedir **defaultvalue** özniteliği:

```cpp
// cpp_attr_ref_defaultvalue.cpp
// compile with: /LD
#include <windows.h>

[export] typedef long HRESULT;
[export, ptr, string] typedef unsigned char * MY_STRING_TYPE;

[  uuid("479B29EE-9A2C-11D0-B696-00A0C903487A"), dual, oleautomation, helpstring("IFireTabCtrl Interface"), helpcontext(122), pointer_default(unique) ]

__interface IFireTabCtrl : IDispatch {
   [bindable, propget] HRESULT get_Size([out, retval, defaultvalue("33")] long *nSize);
   [bindable, propput] HRESULT put_Size([in] int nSize);
};

[ module(name="ATLFIRELib", uuid="479B29E1-9A2C-11D0-B696-00A0C903487A",    version="1.0", helpstring="ATLFire 1.0 Type Library") ];
```

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**İçin geçerlidir**|Parametre arabirimi|
|**Tekrarlanabilir**|Hayır|
|**Gerekli öznitelikleri**|Yok.|
|**Geçersiz öznitelikler**|Yok.|

Daha fazla bilgi için [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>Ayrıca Bkz.

[IDL öznitelikleri](idl-attributes.md)<br/>
[Parametre Öznitelikleri](parameter-attributes.md)<br/>
[out](out-cpp.md)<br/>
[retval](retval.md)<br/>
[in](in-cpp.md)<br/>
[pointer_default](pointer-default.md)<br/>
[benzersiz](unique-cpp.md)  