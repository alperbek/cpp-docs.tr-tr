---
title: length_is (C++ COM özniteliği) | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.technology:
- cpp-windows
ms.topic: reference
f1_keywords:
- vc-attr.length_is
dev_langs:
- C++
helpviewer_keywords:
- length_is attribute
ms.assetid: 1d99b883-84bb-4b1e-b098-eb780fc94f40
author: mikeblome
ms.author: mblome
ms.workload:
- cplusplus
- uwp
ms.openlocfilehash: d412ac93ec9e89de8c85758d98d67fa2a7c50e92
ms.sourcegitcommit: 955ef0f9d966e7c9c65e040f1e28fa83abe102a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48789975"
---
# <a name="lengthis"></a>length_is

Aktarılacak dizi öğelerinin sayısını belirtir.

## <a name="syntax"></a>Sözdizimi

```cpp
[ length_is("expression") ]
```

### <a name="parameters"></a>Parametreler

*İfade*<br/>
Bir veya daha fazla C dili ifadeleri. Boş bağımsız değişken yuvaları izin verilir.

## <a name="remarks"></a>Açıklamalar

**Length_is** C++ özniteliği ile aynı işlevlere sahip [length_is](/windows/desktop/Midl/length-is) MIDL özniteliği.

## <a name="example"></a>Örnek

Bkz: [first_is](first-is.md) örneği nasıl bir dizinin bir bölümünü belirtin.

## <a name="requirements"></a>Gereksinimler

### <a name="attribute-context"></a>Öznitelik bağlamı

|||
|-|-|
|**İçin geçerlidir**|İçinde alan **yapı** veya **birleşim**, parametre arabirim, arabirim yöntemi|
|**Tekrarlanabilir**|Hayır|
|**Gerekli öznitelikleri**|Yok.|
|**Geçersiz öznitelikler**|Yok.|

Daha fazla bilgi için [öznitelik bağlamları](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>Ayrıca Bkz.

[IDL öznitelikleri](idl-attributes.md)<br/>
[Typedef, Enum, Union ve Struct Öznitelikleri](typedef-enum-union-and-struct-attributes.md)<br/>
[Parametre Öznitelikleri](parameter-attributes.md)<br/>
[first_is](first-is.md)<br/>
[max_is](max-is.md)<br/>
[last_is](last-is.md)<br/>
[size_is](size-is.md)  