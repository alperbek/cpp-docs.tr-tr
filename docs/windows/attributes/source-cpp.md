---
title: Kaynak (C++ com özniteliği)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.source
helpviewer_keywords:
- source attribute
ms.assetid: 1878d05d-7709-4e97-b114-c62f38f5140e
ms.openlocfilehash: 5f961513b948c3195aea864d97313ac09e97344e
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80166230"
---
# <a name="source-c"></a>kaynak (C++)

Bir sınıfında, bağlantı noktaları için COM nesnesinin kaynak arabirimlerini belirtir. Bir özellik veya yöntemde, üyenin bir olay kaynağı olan bir nesne veya DEĞIŞKEN döndürdüğünü gösterir.

## <a name="syntax"></a>Sözdizimi

```cpp
[ source(interfaces) ]
```

### <a name="parameters"></a>Parametreler

*arabirimlerdeki*<br/>
Bir sınıfa kaynak özniteliği uyguladığınızda belirttiğiniz bir veya daha fazla arabirim. Bu parametre, kaynak bir özelliğe veya yönteme uygulandığında kullanılmaz.

## <a name="remarks"></a>Açıklamalar

**Kaynak** C++ öznitelik, [kaynak](/windows/win32/Midl/source) MIDL özniteliğiyle aynı işlevselliğe sahiptir.

Bir nesnenin varsayılan kaynak arabirimini belirtmek için [varsayılan](default-cpp.md) özniteliğini kullanabilirsiniz.

## <a name="example"></a>Örnek

```cpp
// cpp_attr_ref_source.cpp
// compile with: /LD
#include "windows.h"
#include "unknwn.h"
[module(name="MyLib")];

[object, uuid(11111111-1111-1111-1111-111111111111)]
__interface b
{
   [id(0), propget, bindable, displaybind, defaultbind, requestedit]
   HRESULT get_I([out, retval]long *i);
};

[object, uuid(11111111-1111-1111-1111-111111111131)]
__interface c
{
   [id(0), propget, bindable, displaybind, defaultbind, requestedit]
   HRESULT et_I([out, retval]long *i);
};

[coclass, default(c), uuid(11111111-1111-1111-1111-111111111132)]
class N : public b
{
};

[coclass, source(c), default(b, c), uuid(11111111-1111-1111-1111-111111111133)]
class NN : public b
{
};
```

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**Uygulama hedefi**|**sınıf**, **Yapı**, **arabirim**|
|**Tekrarlanabilir**|Hayır|
|**Gerekli öznitelikler**|`coclass` (sınıfa veya yapıya uygulandığında)|
|**Geçersiz öznitelikler**|Hiçbiri|

Öznitelik bağlamları hakkında daha fazla bilgi için bkz. [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>Ayrıca bkz.

[IDL öznitelikleri](idl-attributes.md)<br/>
[Sınıf Öznitelikleri](class-attributes.md)<br/>
[Yöntem Öznitelikleri](method-attributes.md)<br/>
[coclass](coclass.md)
