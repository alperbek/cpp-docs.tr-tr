---
title: _callnewh
ms.date: 4/2/2020
api_name:
- _callnewh
- _o__callnewh
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-heap-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _callnewh
helpviewer_keywords:
- _callnewh
ms.assetid: 4dcb73e9-6384-4d12-a973-a8807d4de7a8
ms.openlocfilehash: 3990d4b15c25cfd6c753c2b1d44c112971ff59af
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82918796"
---
# <a name="_callnewh"></a>_callnewh

Şu anda yüklü olan *Yeni işleyiciyi*çağırır.

## <a name="syntax"></a>Sözdizimi

```cpp
int _callnewh(
   size_t size
   )
```

### <a name="parameters"></a>Parametreler

*boyutla*<br/>
[Yeni işlecin](../../cpp/new-operator-cpp.md) ayırmaya çalıştığı bellek miktarı.

## <a name="return-value"></a>Dönüş Değeri

|Değer|Açıklama|
|-----------|-----------------|
|0|Hata: hiçbir yeni işleyici yüklenmedi ya da etkin bir işleyici yok.|
|1|Başarılı: yeni işleyici yüklendi ve etkin. Bellek ayırma yeniden denenebilir.|

## <a name="exceptions"></a>Özel durumlar

Bu işlev, *yeni işleyici* bulunamıyorsa [bad_alloc](../../standard-library/bad-alloc-class.md) atar.

## <a name="remarks"></a>Açıklamalar

Yeni [operatör](../../cpp/new-operator-cpp.md) belleği başarıyla ayıramazsa *yeni işleyici* çağrılır. Yeni işleyici daha sonra sonraki ayırmaların başarılı olması için belleği boşaltma gibi bazı uygun eylemleri başlatabilir.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|_callnewh|iç. h|

## <a name="see-also"></a>Ayrıca bkz.

[_set_new_handler](set-new-handler.md)<br/>
[_set_new_mode](set-new-mode.md)<br/>
