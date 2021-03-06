---
title: CComAutoDeleteCriticalSection sınıfı
ms.date: 11/04/2016
f1_keywords:
- CComAutoDeleteCriticalSection
- atlcore/ATL::CComAutoDeleteCriticalSection
helpviewer_keywords:
- CComAutoDeleteCriticalSection class
ms.assetid: 2396dbea-1c60-4841-b50e-c4e18af311a3
ms.openlocfilehash: d479adce489e0329be3a93b55a70aa3e58a0e038
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62246664"
---
# <a name="ccomautodeletecriticalsection-class"></a>CComAutoDeleteCriticalSection sınıfı

Bu sınıf, alma ve kritik bölüm nesnenin sahipliğini serbest için yöntemler sağlar.

## <a name="syntax"></a>Sözdizimi

```
class CComAutoDeleteCriticalSection : public CComSafeDeleteCriticalSection
```

## <a name="remarks"></a>Açıklamalar

`CComAutoDeleteCriticalSection` sınıfından türetilen [CComSafeDeleteCriticalSection](../../atl/reference/ccomsafedeletecriticalsection-class.md). Ancak, `CComAutoDeleteCriticalSection` geçersiz kılmalar [terimi](ccomsafedeletecriticalsection-class.md#term) yönteme **özel** erişim, yalnızca bu sınıfın örneklerinin kapsam dışına çıkmadan veya açıkça silinir gerçekleşmesi için iç bellek temizleme zorlar bellek.

Bu sınıf, taban sınıfı hiçbir ek yöntemleri tanıtır. Bkz: [CComSafeDeleteCriticalSection](../../atl/reference/ccomsafedeletecriticalsection-class.md) ve [CComCriticalSection](../../atl/reference/ccomcriticalsection-class.md) kritik bölüm yardımcı sınıfları hakkında daha fazla bilgi için.

## <a name="inheritance-hierarchy"></a>Devralma Hiyerarşisi

[CComCriticalSection](../../atl/reference/ccomcriticalsection-class.md)

[CComSafeDeleteCriticalSection](../../atl/reference/ccomsafedeletecriticalsection-class.md)

`CComAutoDeleteCriticalSection`

## <a name="requirements"></a>Gereksinimler

**Başlık:** atlcore.h

## <a name="see-also"></a>Ayrıca bkz.

[CComSafeDeleteCriticalSection Sınıfı](../../atl/reference/ccomsafedeletecriticalsection-class.md)<br/>
[CComCriticalSection Sınıfı](../../atl/reference/ccomcriticalsection-class.md)<br/>
[Sınıfına genel bakış](../../atl/atl-class-overview.md)
