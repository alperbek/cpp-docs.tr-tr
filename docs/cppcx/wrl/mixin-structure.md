---
title: MixIn Yapısı
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- implements/Microsoft::WRL::MixIn
helpviewer_keywords:
- MixIn structure
ms.assetid: 47e2df9b-3a2e-4ae8-8ba3-b1fd3aa73566
ms.openlocfilehash: 16fd6b46d616df7163a304afa7f32ac3c095d398
ms.sourcegitcommit: c7f90df497e6261764893f9cc04b5d1f1bf0b64b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59031082"
---
# <a name="mixin-structure"></a>MixIn Yapısı

Bir çalışma zamanı sınıf varsa Windows çalışma zamanı arabirimleri ve ardından klasik COM arabirimleri türetilen sağlar.

## <a name="syntax"></a>Sözdizimi

```cpp
template<
    typename Derived,
    typename MixInType,
    bool hasImplements = __is_base_of(Details::ImplementsBase, MixInType)
>
struct MixIn;
```

### <a name="parameters"></a>Parametreler

*Türetilmiş*<br/>
Türetilmiş bir tür [uygular](implements-structure.md) yapısı.

*MixInType*<br/>
Bir taban türü.

*hasImplements*<br/>
**doğru** varsa *MixInType* olan geçerli uygulamasından türetilmiş temel tür; **false** Aksi takdirde.

## <a name="remarks"></a>Açıklamalar

Windows çalışma zamanı hem sınıf COM arabirimleri türetilmiş bir sınıf, sınıf bildirimi listesi Windows çalışma zamanı arabirimlerden önce listelemesi gerekir ve ardından tüm klasik COM arabirimleri. **MixIn** arabirimler doğru sırada belirtilir sağlar.

## <a name="inheritance-hierarchy"></a>Devralma Hiyerarşisi

`MixIn`

## <a name="requirements"></a>Gereksinimler

**Başlık:** implements.h

**Namespace:** Microsoft::WRL

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft::WRL Ad Alanı](microsoft-wrl-namespace.md)